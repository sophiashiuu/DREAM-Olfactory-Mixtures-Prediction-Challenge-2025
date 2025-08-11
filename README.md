# 🌸 DREAM Olfactory Mixtures Prediction Challenge 2025

## 📌 Background & Motivation
Predicting human olfactory perception from chemical structure is a major challenge in computational neuroscience. While molecular descriptors capture structural information, translating these into accurate perceptual predictions remains difficult.

Our goals were to:  
- **Predict perceptual ratings** for single molecules (**Task 1**) and mixtures (**Task 2**)  
- **Use Random Forest Regression** for its balance of interpretability, robustness, and ability to handle high-dimensional molecular data  
- **Integrate diverse molecular features** to improve generalization to unseen compounds and mixtures  

| **Feature Source**            | **Description**                                   |
|--------------------------------|---------------------------------------------------|
| **Mordred descriptors**        | Physicochemical and structural molecular features |
| **Morgan fingerprints**        | Circular substructure fingerprints                |
| **OpenPOM perceptual vectors** | Human perceptual data projections                 |

---

## 🛠 Methods

### **Task 1 – Single-Molecule Prediction**  
**📂 Data Integration**  
- Merged `TASK1_Stimulus_definition.csv` with `Mordred_Descriptors.csv` on **molecule**  
- Combined with `TASK1_training.csv` on **stimulus**  

**🔍 Feature Selection**  
- Removed non-numeric and metadata columns (`stimulus`, `molecule`, `dilution`, etc.)  

**⚙ Preprocessing**  
- Replaced infinite values with `NaN`, missing values with `0`  
- Scaled features with `StandardScaler`  

**🤖 Model**  
- `RandomForestRegressor` wrapped in `MultiOutputRegressor`  
- Hyperparameters: `n_estimators=100`, `random_state=42`  
- Train-validation split: **80/20**  

**📏 Evaluation Metric**  
- Root Mean Squared Error (**RMSE**)  

---

### **Task 2 – Mixture Prediction**  
**📂 Data Integration**  
- Merged `Mordred_Descriptors.csv` and `Morgan_fingerprints.csv` on **molecule**  
- Added SMILES strings and `OpenPOM_Dream_RATA.csv` perceptual data  

**🧩 Component Aggregation**  
- Linked component-level features to stimuli  
- Averaged numeric features per mixture  
- Missing values → zeros  

**⚙ Preprocessing**  
- Scaled features using training set statistics  

**🤖 Model**  
- Same setup as Task 1  
- Train-validation split: **90/10**  

**📏 Evaluation Metrics**  
- RMSE  
- Mean Cosine Distance  
- Mean Pearson Correlation  

## 📊 Tools & Libraries
* Python 3.11

* pandas, numpy — data wrangling

* scikit-learn — modeling & evaluation

## 📈 Results & Discussion
Task 1 was easier to model due to direct molecule-descriptor mapping while Task 2 required aggregation of multiple molecular representations for mixtures. At the end, we came to terms that combining diverse molecular features improved generalization.

Major challenge: missing features for some components, handled via zero imputation.

## 📌 Future work:
Capture interactions between mixture components.
Go beyond simple averaging for mixture representation.

## 📝 License
This project is for educational and event purposes at the University of Michigan- Ann Arbor (DREAM Olfactory Mixtures Prediction Challenge 2025).


## 🙏 Acknowledgments
Thanks to the dataset and research providers for support and guidance.

1. Boldini, D., Ballabio, D., Consonni, V., Todeschini, R., Grisoni, F., & Sieber, S. A. (2024, March 25). Effectiveness of molecular fingerprints for exploring the chemical space of natural products. Journal of cheminformatics. https://pmc.ncbi.nlm.nih.gov/articles/PMC10964529/ 
2. Megalakaki, O., Ballenghein, U., & Baccino, T. (2019, February 1). Effects of valence and emotional intensity on the comprehension and memorization of texts. Frontiers in psychology. https://pmc.ncbi.nlm.nih.gov/articles/PMC6367271/ 
3. U.S. Department of Health and Human Services. (2025a, May 8). How the nose decodes complex odors. National Institutes of Health. https://www.nih.gov/news-events/nih-research-matters/how-nose-decodes-complex-odors 
4. DREAM Olfactory Mixtures Prediction Challenge 2025 (syn64743570)


