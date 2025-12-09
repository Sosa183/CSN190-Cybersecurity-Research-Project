Which Project I Cloned

I cloned the “Using-machine-learning-to-detect-malicious-URLs” repository, which provides a classic machine-learning baseline for detecting malicious URLs using Python, scikit-learn, and a labeled dataset. This served as the foundation for building, testing, and documenting my own phishing detection workflow.

Steps I Followed

I began by cloning the project into PyCharm, installing Python 3.x, and setting up all required dependencies through the REQUIREMENTS file. After confirming that the dataset (data.csv) was available in the data/ folder, I opened the training script and explored how the model loads the data, extracts features, and performs classification. I then ran the script to generate predictions, reviewed the outputs, and documented every step. Finally, I experimented with the optional API server, which allows URL classification through a local web endpoint.

Commands I Ran

git clone https://github.com/Sosa183/Using-machine-learning-to-detect-malicious-URLs

python -m pip install --upgrade pip

python -m pip install -r REQUIREMENTS

python my_url_classifier.py

(optional) python AIserver.py

Problems and Solutions

I ran into several environment issues during setup.

Problem: pip not recognized → Solution: Used python -m pip to install dependencies correctly.

Problem: Missing libraries like Flask, numpy, and scikit-learn → Solution: Installed each package manually using python -m pip install <package>.

Problem: Project wouldn’t run because Python wasn’t linked on PATH → Solution: Installed Python from Microsoft Store and restarted terminal.
Each of these errors helped me understand Python environments, dependency management, and debugging techniques.
