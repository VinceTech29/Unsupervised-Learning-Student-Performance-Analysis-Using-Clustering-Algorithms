# Student Performance Analysis Using Clustering Algorithms

An end-to-end unsupervised machine learning project analyzing student academic behaviors and performance patterns using four clustering methodologies: **K-Means Clustering**, **Fuzzy C-Means (FCM)**, **Gaussian Mixture Models (GMM)**, and **Hierarchical Agglomerative Clustering**.

---

## 📌 Project Overview

Understanding student learning dynamics is crucial for educational institutions seeking to improve retention rates, allocate teaching resources efficiently, and offer personalized interventions. This project investigates student performance across multidimensional behavioral and academic metrics—including **Study Hours**, **Examination Scores**, and **Class Attendance**—to uncover natural groupings without relying on predefined labels.

By applying both partitioning, fuzzy, probabilistic, and hierarchical paradigms, the project compares how different mathematical assumptions capture student cohorts and translates machine learning findings into concrete, actionable institutional strategies.

---

## 🎯 Objectives

1. **Unsupervised Cohort Discovery**: Segment a cohort of 14,003 students based on key academic performance metrics.
2. **Multi-Algorithm Comparative Analysis**: Implement and evaluate four fundamental clustering algorithms on identical academic data:
   - Partitioning Clustering: **K-Means**
   - Soft / Fuzzy Clustering: **Fuzzy C-Means (FCM)**
   - Probabilistic Clustering: **Gaussian Mixture Models (GMM)**
   - Connectivity Clustering: **Hierarchical Agglomerative Clustering**
3. **Multi-Resolution Hierarchy**: Utilize dendrogram visualization to determine optimal structural divisions (confirming 3 natural macro-clusters at distance threshold $y = 600$).
4. **Actionable Business & Educational Interventions**: Provide at least two strategic institutional decisions per cluster to drive retention, honors incubation, and early-warning alerts.

---

## 📊 Dataset Description

The analysis is conducted on the comprehensive **Student Performance Dataset** (`student_performance.csv`) containing records for **14,003 students** across **16 academic, behavioral, and demographic features**:

| Feature Name | Type | Description |
| :--- | :---: | :--- |
| `StudyHours` | Integer | Weekly study hours logged by the student (Mean $\approx 20$ hrs/wk). |
| `Attendance` | Integer | Class attendance percentage ($60\% - 100\%$). |
| `Resources` | Binary | Access to learning resources (0 = Limited, 1 = Adequate). |
| `Extracurricular` | Binary | Participation in extracurricular school activities. |
| `Motivation` | Categorical | Self-reported academic motivation level. |
| `Internet` | Binary | Availability of high-speed internet at home. |
| `Gender` | Binary | Student gender code. |
| `Age` | Integer | Age of student (19 to 28+). |
| `LearningStyle` | Categorical | Preferred learning modality (Visual, Auditory, Kinesthetic). |
| `OnlineCourses` | Integer | Number of completed online support courses. |
| `Discussions` | Binary | Active participation in academic forums and discussion boards. |
| `AssignmentCompletion` | Integer | Percentage of completed homework assignments ($50\% - 100\%$). |
| `ExamScore` | Integer | Final standardized examination score ($40 - 100$ pts). |
| `EduTech` | Binary | Use of educational technology platforms in daily study. |
| `StressLevel` | Categorical | Self-reported stress level. |
| `FinalGrade` | Categorical | Assigned course grade band (0 to 3). |

*Primary Feature Pairs Selected*:
- **StudyHours vs. ExamScore**: Evaluates study efficiency vs. examination outcomes (K-Means, FCM, GMM).
- **StudyHours vs. Attendance**: Assesses behavioral compliance and physical presence vs. self-study investment (Hierarchical Clustering).

---

## 🛠️ Technologies & Libraries

- **Language**: Python 3.10+ / 3.11 / 3.12 / 3.13
- **Data Manipulation**: `pandas`, `numpy`
- **Scientific & Statistical Computing**: `scipy`
- **Machine Learning & Modeling**: `scikit-learn`, `scikit-fuzzy`
- **Data Visualization**: `matplotlib`, `seaborn`
- **Environment**: Visual Studio Code (VS Code), Jupyter Notebooks

---

## 🔬 Clustering Algorithms Implemented

### 1. K-Means Clustering (`01_KMeans_Clustering.ipynb`)
- **Type**: Centroid-based hard partitioning.
- **Features**: `StudyHours` and `ExamScore`.
- **Model**: `KMeans(n_clusters=4, random_state=42, n_init='auto')`.
- **Key Output**: Identifies 4 distinct performance strata: High Achievers (Centroid: 20.13 hrs, 92.11 pts), Competent (19.87 hrs, 75.46 pts), Moderate/Borderline (19.92 hrs, 60.04 pts), and Underperforming (20.01 hrs, 45.83 pts).
- **Visual Result**: [kmeans_results.png](results/kmeans/kmeans_results.png)

### 2. Fuzzy C-Means Clustering (`02_Fuzzy_CMeans_Clustering.ipynb`)
- **Type**: Soft clustering based on fuzzy set membership.
- **Features**: `StudyHours` and `ExamScore`.
- **Model**: `skfuzzy.cmeans(c=3, m=2.0, error=0.005, maxiter=1000)`.
- **Key Output**: Generates continuous membership grades ($u_{ij} \in [0, 1]$) allowing identification of boundary students between grade brackets (Centroids: 49.17 pts, 69.87 pts, 91.09 pts).
- **Visual Result**: [fuzzy_cmeans_results.png](results/fuzzy_cmeans/fuzzy_cmeans_results.png) with $2\sigma$ distribution ellipses.

### 3. Gaussian Mixture Model (GMM) (`03_Gaussian_Mixture_Model.ipynb`)
- **Type**: Probabilistic generative model with full covariance estimation.
- **Features**: `StudyHours` and `ExamScore`.
- **Model**: `GaussianMixture(n_components=4, covariance_type='full', random_state=42)`.
- **Key Output**: Provides Bayesian posterior responsibilities $P(C=k|\mathbf{x})$, enabling risk quantification and objective confidence scoring for scholarship awards.
- **Visual Result**: [gaussian_mixture_results.png](results/gaussian_mixture/gaussian_mixture_results.png) with component means and bivariate Gaussian density contours.

### 4. Hierarchical Agglomerative Clustering (`04_Hierarchical_Clustering.ipynb`)
- **Type**: Connectivity-based bottom-up agglomerative clustering.
- **Features**: `StudyHours` (Feature 1) and `Attendance` (Feature 2).
- **Model**: `AgglomerativeClustering(n_clusters=4, linkage='ward')`.
- **Dendrogram Evaluation**: Truncated linkage tree (`scipy.cluster.hierarchy`).
- **Threshold Cut**: Setting the horizontal threshold line at **$y = 600$** intersects exactly **3 vertical branches**, demonstrating **three natural macro-clusters** across attendance and study behaviors.
- **Visual Results**:
  - [hierarchical_dendrogram.png](results/hierarchical/hierarchical_dendrogram.png)
  - [hierarchical_results.png](results/hierarchical/hierarchical_results.png)

---

## 📁 Repository Structure

```
Student-Performance-Clustering-Analysis/
│
├── README.md                                  # Main project documentation and overview
│
├── notebooks/                                 # Executable Jupyter Notebooks
│   ├── 01_KMeans_Clustering.ipynb             # K-Means implementation & cluster analysis
│   ├── 02_Fuzzy_CMeans_Clustering.ipynb       # Fuzzy C-Means with membership ellipses
│   ├── 03_Gaussian_Mixture_Model.ipynb        # GMM with probabilistic density contours
│   └── 04_Hierarchical_Clustering.ipynb       # Agglomerative clustering & dendrogram cut
│
├── datasets/                                  # Project datasets
│   └── student_performance.csv                # Complete dataset (14,003 records, 16 features)
│
├── results/                                   # High-resolution saved visualizations
│   ├── kmeans/
│   │   └── kmeans_results.png                 # K-Means centroid scatter plot
│   ├── fuzzy_cmeans/
│   │   └── fuzzy_cmeans_results.png           # FCM distribution ellipses & centroids
│   ├── gaussian_mixture/
│   │   └── gaussian_mixture_results.png       # GMM 2-sigma density contours & component means
│   └── hierarchical/
│       ├── hierarchical_dendrogram.png        # Ward linkage dendrogram with y=600 threshold
│       └── hierarchical_results.png           # 2D scatter plot of cluster assignments
│
├── documentation/                             # In-depth analytical documentation
│   ├── Cluster_Interpretations.md             # Detailed breakdown of cluster characteristics
│   ├── Business_Decisions.md                  # Strategic institutional recommendations (2+ per cluster)
│   └── Clustering_Comparison.md               # Technical algorithm comparison & trade-off matrix
│
├── requirements.txt                           # Python package dependencies
└── .gitignore                                 # Git ignore patterns for clean commits
```

---

## 🚀 Setup & Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/<your-username>/Student-Performance-Clustering-Analysis.git
cd Student-Performance-Clustering-Analysis
```

### Step 2: Create and Activate a Virtual Environment
```bash
# Windows (PowerShell)
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
```

### Step 3: Install Required Dependencies
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

---

## 💻 Running the Project in VS Code

1. **Open the Project in VS Code**:
   ```bash
   code .
   ```
2. **Select Python Kernel**:
   - Open any notebook inside `notebooks/` (e.g., `01_KMeans_Clustering.ipynb`).
   - Click **Select Kernel** in the upper right corner of VS Code.
   - Choose your activated virtual environment (`.venv` or local Python 3.x).
3. **Execute Notebooks**:
   - Click **Run All** to execute all cells sequentially.
   - All dataset paths dynamically adapt to relative directory structures (`../datasets/student_performance.csv` or project root).
   - Generated plots automatically save to their designated folders in `results/`.

---

## 💡 Key Findings

1. **Study Hours Independence**: Across all four algorithms, mean study hours hover uniformly between **19.8 and 20.1 hours/week**, indicating that sheer study volume does not guarantee academic success. Study methodology, foundational mastery, and engagement are the true differentiators.
2. **Fuzzy Transitions Over Rigid Boundaries**: Fuzzy C-Means demonstrates that ~33% of students reside in borderline capability zones ($u_i \approx 0.45 - 0.55$), proving that soft clustering provides more nuanced metrics for academic progression.
3. **Probabilistic Risk Triaging**: GMM's posterior probability allows institutions to define risk thresholds (e.g., $P(\text{At-Risk}) > 0.50$) for automated counselor assignment.
4. **Hierarchical Attendance Structure**: The dendrogram cut at threshold **$y = 600$** reveals **3 natural macro-clusters**, showing that attendance habits form deep structural divisions in student cohorts.

---

## 📄 Documentation Links

- Detailed cluster breakdowns: [Cluster_Interpretations.md](documentation/Cluster_Interpretations.md)
- Strategic institutional interventions: [Business_Decisions.md](documentation/Business_Decisions.md)
- Comprehensive mathematical & algorithmic comparison: [Clustering_Comparison.md](documentation/Clustering_Comparison.md)

---

## 📜 License & Acknowledgments

This project is prepared for educational and research analysis into unsupervised learning methodologies in academic performance analytics. Feel free to use and extend this codebase for academic research and institutional planning.
