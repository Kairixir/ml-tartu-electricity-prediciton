# Training settings

```python
LOAD = (
    True  # True = load previously saved model from disk?  False = (re)train the model
)
SAVE = "transformer.tar"  # file name to save the model under

EPOCHS = 50
INLEN = 32  # input size
FEAT = 16  # d_model = number of expected features in the inputs, up to 512
HEADS = 4  # default 8
ENCODE = 6  # encoder layers
DECODE = 6  # decoder layers
DIM_FF = 128  # dimensions of the feedforward network, default 2048
BATCH = 32  # batch size
ACTF = "relu"  # activation function, relu (default) or gelu
SCHLEARN = None  # a PyTorch learning rate scheduler; None = constant rate
LEARN = 1e-3  # learning rate
VALWAIT = 1  # epochs to wait before evaluating the loss on the test/validation set
DROPOUT = 0.1  # dropout rate
N_FC = 1  # output size

RAND = 42  # random seed
N_SAMPLES = 100  # number of times a prediction is sampled from a probabilistic model
N_JOBS = -1  # parallel processors to use;  -1 = all processors

# default quantiles for QuantileRegression
QUANTILES = [0.01, 0.1, 0.2, 0.5, 0.8, 0.9, 0.99]

FIGSIZE = (9, 6)


qL1, qL2 = 0.01, 0.10  # percentiles of predictions: lower bounds
qU1, qU2 = (
    1 - qL1,
    1 - qL2,
)  # upper bounds derived from lower bounds
label_q1 = f"{int(qU1 * 100)} / {int(qL1 * 100)} percentile band"
label_q2 = f"{int(qU2 * 100)} / {int(qL2 * 100)} percentile band"

mpath = os.path.abspath(os.getcwd()) + SAVE  # path and file name to save the model

model = TransformerModel(
    input_chunk_length=INLEN,
    output_chunk_length=N_FC,
    batch_size=BATCH,
    n_epochs=EPOCHS,
    model_name="Transformer_consumption",
    nr_epochs_val_period=VALWAIT,
    d_model=FEAT,
    nhead=HEADS,
    num_encoder_layers=ENCODE,
    num_decoder_layers=DECODE,
    dim_feedforward=DIM_FF,
    dropout=DROPOUT,
    activation=ACTF,
    random_state=RAND,
    likelihood=QuantileRegression(quantiles=QUANTILES),
    optimizer_kwargs={"lr": LEARN},
    add_encoders={"cyclic": {"future": ["hour", "weekday", "month"]}},
    save_checkpoints=True,
    force_reset=True,
    pl_trainer_kwargs = {"accelerator": "cpu"},
)
```