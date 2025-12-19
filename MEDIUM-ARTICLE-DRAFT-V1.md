Can My Laptop Catch Phishing Links? Building a Machine Learning URL Detector in PyCharm

<img width="1200" height="600" alt="image" src="https://github.com/user-attachments/assets/0856fa7b-aa22-43e1-9948-ecce7aba77ad" />


If you’ve ever hovered over a sketchy link in your inbox and wondered, “Is this safe to click?”, you’re not alone. Phishing attacks are still one of the easiest ways for attackers to break into accounts, steal money, and compromise entire organisations. Instead of trying to memorise every red flag by hand, I wanted to see what would happen if I taught my laptop to spot bad links for me.

In this article, I’ll walk you through my first hands-on project, building an AI-powered phishing detection system using a public GitHub repository called “Using machine learning to detect malicious URLs” by Faizan Ahmad. I ran everything inside PyCharm on my own machine, starting from cloning the repo and installing dependencies all the way to training models and testing them on real URLs.

By the end of this article, you’ll see:
- How I set up a basic machine learning pipeline for malicious URL detection
- What features does the model use to tell “normal” links from “phishy” ones
- How well the model actually performed on test data
- What I learned from research papers and industry reports about phishing attacks
- Where I struggled, how I fixed errors, and what I’d do differently next time

I’m writing this as a cybersecurity student still learning, not as an expert. If you’re curious about phishing, machine learning, or just want a realistic beginner project you can reproduce in PyCharm, this walkthrough is for you.
 Purpose 
I chose phishing detection because it sits right at the intersection of security and machine learning. Almost every major breach report mentions phishing, and I wanted to go beyond the theory and actually build something that could classify URLs as “malicious” or “benign.”

The specific tool I chose to work with is the GitHub project “Using machine learning to detect malicious URLs” by Faizan Ahmad (faizann24). This repo implements a classic machine-learning pipeline using URL-based features (length, number of dots, special characters, etc.) and traditional classifiers like Logistic Regression and Random Forest. It’s not a fancy transformer or deep-learning system, but that’s exactly why I picked it: it’s a solid, understandable baseline I can actually run and modify.

From a cybersecurity perspective, this tool aims to solve a very practical problem: given a URL, can we decide if it’s likely phishing/malicious before the user clicks it? Security teams, email gateways, and browser vendors all care about this problem because blocking a malicious link at the URL layer is often faster and cheaper than dealing with a full incident later.

My personal goals were to learn how a real phishing-detection dataset is structured; see how features are engineered from raw URLs; train and evaluate at least one model, then inspect the results; and build confidence working with Python, scikit-learn, and datasets in PyCharm.

At first, I was a little intimidated—machine learning can feel like magic from the outside. I expected to be overwhelmed by math and theory. What actually happened was more down-to-earth: I spent most of my time dealing with imports, dependencies, and understanding how the data was cleaned. Once that was under control, experimenting with models felt much more approachable.

This project also gave me a concrete foundation for my larger topic: AI-Powered Phishing Detection Systems, where this URL classifier could be one component of a bigger, more modern pipeline.
 Installation and Setup Tutorial
In this section, I’ll show you how I got the malicious-URL project running in PyCharm. You can follow the same steps on your own computer.

Prerequisites:
- A computer with Windows, macOS, or Linux
- Python 3.x installed
- PyCharm (Community Edition is fine)
- Git installed (or you can download the ZIP from GitHub)

Step 1: Clone the GitHub Repository
I opened a terminal and ran:
git clone https://github.com/faizann24/Using-machine-learning-to-detect-malicious-URLs.git
cd Using-machine-learning-to-detect-malicious-URLs

<img width="828" height="783" alt="image" src="https://github.com/user-attachments/assets/08fb4b6e-7ef6-43df-8770-0f1687b296b7" />

Step 2: Open the Project in PyCharm
I opened PyCharm, clicked “Open,” and selected the project folder. PyCharm detected the project and created a Python interpreter for it.

<img width="687" height="365" alt="image" src="https://github.com/user-attachments/assets/e7cad739-7a07-4f87-bfdb-c435226bf1dc" />

Step 3: Install Dependencies
Inside PyCharm’s Terminal, I used Python’s module form of pip so I didn’t have to worry about PATH issues:
python -m pip install --upgrade pip
python -m pip install numpy pandas scikit-learn matplotlib flask

<img width="828" height="473" alt="image" src="https://github.com/user-attachments/assets/92edd890-ee27-4fd1-858d-cd76ab6cf4f6" />

If the repo had extra requirements, I installed them the same way. Any missing package error from a script was fixed by running python -m pip install <packagename>.

Step 4: Explore the Code and Dataset
In the project pane, I opened data/data.csv to see the URLs and labels (good/bad), and
 looked at the main Python file to understand how the model was trained. This made the rest of the steps much less mysterious.

<img width="828" height="753" alt="image" src="https://github.com/user-attachments/assets/0de3e1b4-a1bd-4389-a12c-74c46735436a" />

 Using the Software
Instead of listing all the things this project could do, here’s exactly what I did: I trained a model and then used it to predict whether a small list of URLs was malicious or benign.

First, I ran the training code from the repo to load the dataset, extract features from the raw URLs, train a machine learning model, and evaluate it on a test set. The core of the pipeline used a TfidfVectorizer over URL tokens and a Logistic Regression classifier. Once training was completed, the script printed the test accuracy and a basic evaluation.

<img width="828" height="423" alt="image" src="https://github.com/user-attachments/assets/e049e77f-6a3b-4840-b550-d851e5d26c7c" />

Then I created my own Python file in PyCharm to act as a tiny phishing-detector tool. It loaded the trained model, took a list of URLs like https://accounts.google.com/ServiceLogin and http://login-secure-paypal.com.verify-details.xyz/login, transformed them using the same vectorizer, and asked the model to predict a label for each one.

For obviously fake-looking domains, the model usually predicted the malicious label, while well-known domains like https://accounts.google.com/ tended to be labelled benign. Seeing this in action made the project feel real: my laptop was classifying URLs similarly to how a basic email security filter might behave.

<img width="828" height="533" alt="image" src="https://github.com/user-attachments/assets/07cb1154-3259-4ffc-9abb-cff5baa52b96" />

<img width="1100" height="563" alt="image" src="https://github.com/user-attachments/assets/6bcb3327-e697-4f3c-91a1-3781676d223d" />

Behind the scenes, the model wasn’t reading page content — it relied purely on URL-based signals such as length, character patterns, and token structure. That’s powerful enough to catch a lot of noisy, low-effort phishing links, but it also showed me where URL-only detection has limitations.

 Research Insights
To connect my hands-on work with the bigger picture, I looked at two main sources: one academic paper and one industry report.

The first was Haq, Q. E., Sadiq, S., Shafique, A., & Farooq, M. (2024). Detecting phishing URLs based on a deep learning approach using 1D-CNN. Applied Sciences, 14(22), 10086. The paper proposes a 1D convolutional neural network that operates directly on URL strings. Instead of hand-crafted features, the model learns character-level patterns on its own and achieves strong accuracy on public datasets. Reading this after working with the classic GitHub repo helped me see where my project fits: my baseline uses traditional feature engineering and classical ML, while the paper’s approach shows how deep learning can remove some of that manual work and potentially generalise better to new attacks.

The second source was the Anti-Phishing Working Group’s Phishing Activity Trends Report (Q2 2025). This industry report tracks over a million phishing attacks in a single quarter, breaking down targeted sectors, lures, and techniques. One thing that stood out was how often attackers rotate infrastructure—domains and URLs—to stay ahead of static blocklists.

Together, these sources shifted my perspective from “I built a cool URL classifier” to understanding that this is one component in a constantly evolving battle. The research paper shows how model architectures are evolving, while the APWG report shows how the threats themselves keep changing. A real AI-powered phishing detection system has to keep up with both.
 Challenges and Problem-Solving
Nothing about this project was just “click and run.” I ran into several problems, and honestly, that’s where most of the learning happened.

The first issue was the environment and dependency problems. On Windows, pip wasn’t recognised at first, so I had to switch to using python -m pip and carefully install the needed libraries inside PyCharm’s terminal. Some versions of scikit-learn and other packages did not match what the original project expected, so I fixed errors by reading tracebacks, installing missing packages, and occasionally downgrading or upgrading specific libraries.

Another challenge was understanding the feature-engineering code. The original project used a custom tokeniser for URLs, splitting on characters like '/', '-', and '.', then feeding that into TF-IDF. At first, it was just a wall of code. I added print statements and tested the tokeniser on a single URL to see exactly which tokens it was creating. Once I did that, I understood why certain URLs were easier or harder for the model to classify.

Finally, wiring my own testing script to the trained model required reusing the same preprocessing steps. Any mismatch between how the model was trained and how I prepared new URLs would cause errors or nonsense output. Fixing that taught me how important consistency is in machine learning pipelines.

Each error was frustrating in the moment, but solving them made me more confident reading other people’s code, using AI tools like ChatGPT for debugging help, and not giving up just because Python threw a scary stack trace.

<img width="700" height="480" alt="image" src="https://github.com/user-attachments/assets/d6c3cb04-6b68-47a8-86e1-b9a739adac89" />

 Conclusion and Future Applications
By the time I finished this project, I had done much more than just run a script from GitHub. I had cloned and set up a real-world machine learning project in PyCharm, installed and managed dependencies, trained a malicious URL classifier on a real dataset, tested it on custom URLs, and connected my practical results with research papers and industry reports.

The biggest lesson was that AI-powered phishing detection is not magic. It is a pipeline of very human steps: collecting data, cleaning it, choosing features or architectures, training models, evaluating results, and dealing with things breaking at every stage. Seeing the model successfully flag obviously bad URLs gave me a sense of what’s possible, but it also reminded me that no single layer is enough.

In terms of skills, I improved both technical and soft skills. On the technical side, I practised Python, scikit-learn, working with CSV datasets, and integrating machine learning code into a small tool. On the soft skills side, I practised troubleshooting, reading documentation, and using AI assistants strategically instead of copy-pasting random code.

Looking ahead, I would like to implement a 1D-CNN URL model based on the Haq et al. paper and compare it directly against this baseline. I’m also interested in integrating this kind of URL detector into a broader email-analysis pipeline that looks at sender information, headers, and even landing-page content. Eventually, I could see this being one building block inside a larger Zero-Trust Architecture where every link and request is continuously evaluated.

For now, this project gave me a realistic first step into AI-powered phishing detection and something concrete I can show as part of my cybersecurity portfolio.
 Resources and Links
My Work:
-https://github.com/Sosa183/Using-machine-learning-to-detect-malicious-URLs 

Software and Tools:
- Baseline tool GitHub: https://github.com/Sosa183/Using-machine-learning-to-detect-malicious-URLs  
- PyCharm: https://www.jetbrains.com/pycharm/ 
- Python: https://www.python.org/downloads/ 

Research Sources:
-   Safi, A., Jhanjhi, N. Z., Humayun, M., & others. (2023). A systematic literature review on phishing website detection techniques. Journal of King Saud University – Computer and Information Sciences.
 Comprehensive survey of machine-learning methods for phishing website detection, especially URL and HTML-based features. https://www.sciencedirect.com/science/article/pii/S1319157823000034?utm_source=chatgpt.com

- Haq, Q. E., Sadiq, S., Shafique, A., & Farooq, M. (2024). Detecting phishing URLs based on a deep learning approach using 1D-CNN. Applied Sciences, 14(22), 10086. https://www.mdpi.com/2076-3417/14/22/10086?utm_source=chatgpt.com 
- https://www.youtube.com/watch?v=9sC3t-g3iJA
- https://github.com/faizann24/Using-machine-learning-to-detect-malicious-URLs
Learning Resources:
- Scikit-learn documentation: https://scikit-learn.org/ 
- Basic phishing awareness resources from organisations like CISA and NIST
- AI tools used for debugging and explanation
