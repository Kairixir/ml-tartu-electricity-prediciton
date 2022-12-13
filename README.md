# ml-tartu-electricity-prediciton
https://www.kaggle.com/competitions/predict-electricity-consumption/overview

# Commit guidelines
https://gist.github.com/ericavonb/3c79e5035567c8ef3267

# Install instructions
1. Create a virtual environment using `python -m venv env`
2. Install dependencies `pip install -r requirements.txt`
    - If you want to train using GPU 
        1. While using cuda 11.3 write `pip install -r requirements-cuda113.txt` instead
        1. Make sure your `torch` installations matches `cuda` installed on your server
        2. Do not use `cuda` version `10.2` [(error in multiplication)](https://stackoverflow.com/questions/66600362/runtimeerror-cuda-error-cublas-status-execution-failed-when-calling-cublassge) [(minimal example to test)](https://github.com/pytorch/pytorch/issues/64097)
3. Enlist virtual environment as usable jupyter kernel `python -m ipykernel --user --name <name-of-kernel>`
4. Run JupyterServer and your Jupyter IDE
5. Make sure the notebook uses your `<name-of-kernel>` kernel for execution

# Important
LSTM code is in lstm branch
