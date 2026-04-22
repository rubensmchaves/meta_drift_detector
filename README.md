# Drift meta learning

The objective is to perform drift detection using meta learning by predicting the performance of a base classification model with unknown target (delayed).

## 1. To Do
- [x] Offline stage MetaLearner implementation
- [x] Online stage MetaLearner implementation
- [x] Meta model incremental learning
- [x] Statistical meta features implementation
- [x] Clustering meta features implementation
- [x] PSI implementation
- [x] Domain classifier implementation
- [x] Meta/base model hyperparameter tuning
- [x] TimeSeries cross validation usage
- [x] Different base model metrics (meta labels) experiments
- [x] Target delay experiments
- [x] Different base model experiments
- [x] Meta base dimensionality reduction experiments
- [x] Other drift metrics implementation
- [x] Other databases experiments
- [x] Measure elapsed time
- [ ] Meta feature selection experiments
- [x] Baseline
- [x] Evaluation metrics for meta model vs baseline
- [x] Drift alert definition
- [x] Drift alert configuration
- [x] Code documentation
- [ ] Readme
- [x] Experiments notebooks adjustments to fit new MetaLearner structure

## 2. Running
To work on this project is important to read the git good practive guide first, [here](https://github.com/rubensmchaves/drift-meta-learning.feamelo/blob/main/git_good_practice.md). For the following steps we consider that you are using a Linux like shell. 

1. Clone this github project.
2. Set a local environment, using `venv` module. Check the W3School tutorial [here](https://www.w3schools.com/python/python_virtualenv.asp).
3. Install the required libraries.
4. Run the project locally.
5. Close the local environment

### 2.1 Clone the project
It is important to note that, if you are using Windows this project has files with special character like ":" in its name. So, if you use the WSL (Windows Subsystem for Linux), otherwise you are going to have problem to checkout the project.

The checkout command:

```
git clone [git_project_url]
```

### 2.2 Local environment
Setting your local environment using the module `venv`. Execute only once, when you set your project for the first time. We suggest to name you local enviroment as `.venv`. Add you source code `src` to the `PYTHONPATH`.

```
python -m venv .venv
echo 'export PYTHONPATH=src' >> .venv/bin/activate
```

Once it is done, verify the prefix `.venv` (your local environment name) at the command prompt, something like:

```
(.venv) feamelo@my_computer:/$
```

If it is not there, start your environment with the command:

```
source .venv/bin/activate
```

### 2.3 Required libraries
Installing the required libraries through the file `requeriments.txt`. At you project root type:

```
pip install -r requirements-minimal.txt
```

### 2.4 Executing 

### 2.5 Close the local environment 
Just run the `venv` command:
```
deactivate
```

## 3. Troubleshooting

###  3.1 Building `wheel` for [...] did not run successfully.
This error is a classic "expert-level" hurdle in Linux. The problem isn't your Python code; it's that your **WSL/Ubuntu** environment is missing the **C/C++ compilers** and **system development libraries** needed to build certain Python packages (like `cffi`, `kiwisolver`, and `Pillow`) from source.

The error logs highlight three main missing pieces:

1. `x86_64-linux-gnu-gcc` **not found**: You don't have the C compiler.
2. `libffi` **not found**: Missing the Foreign Function Interface library.
3. `zlib` **not found**: Missing the compression library required for image processing in `Pillow`.

Many Machine Learning libraries (especially older versions or specific research forks) don't provide "Wheels" (pre-compiled binaries) for every single version of Python (you are using **Python 3.12**). When a Wheel isn't available, `pip` tries to build the package from the source code, which requires a C compiler and system libraries to be present on your Linux machine.

#### The Solution: Install System Dependencies
To fix this for your **Meta-Learning** project, you need to use `sudo` to install the essential build tools and specific header files. Run the following command in your terminal:

```
sudo apt update && sudo apt install -y build-essential libffi-dev python3-dev zlib1g-dev libjpeg-dev
```

Breakdown of what this does:
* `build-essential`: Installs `gcc`, `g++`, and `make`. This solves the "No such file or directory" error for the compiler.
* `libffi-dev`: Provides the headers for `cffi`.
* `python3-dev`: Provides the header files for Python C extensions.
* `zlib1g-dev` & `libjpeg-dev`: Essential for compiling `Pillow` so it can handle compressed images.

#### Step-by-Step Recovery
Once the system packages are installed, try to install your project again. It is often best to clear the "failed" state in your virtual environment:

1. Activate your environment (if not already):

```
source .venv/bin/activate
```

2. Upgrade `pip`, `setuptools`, and `wheel`: This ensures you have the latest building logic.

```
pip install --upgrade pip setuptools wheel
```

3. Re-run your installation:

```
pip install -r requirements.txt
# OR, if you are installing the current folder:
pip install -e .
```
