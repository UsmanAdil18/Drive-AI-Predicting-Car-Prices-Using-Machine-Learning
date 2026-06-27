# 🚗 Drive AI — Predicting Car Prices Using Machine Learning

A Full-Stack Machine Learning Web Application that predicts the prices of **Used**, **New**, and **Imported** cars in Pakistan.  
Built as a **Final Year Project (FYP)** for the BS Computer Science program at the University of Karachi.

---

## 📌 Project Overview

In Pakistan's growing used car market, buyers and sellers often rely on brokers who manipulate prices — leaving both parties at a disadvantage. **Drive AI** solves this problem by providing an ML-powered platform that gives instant, data-driven price estimates for any type of car.

Whether you're a **buyer**, **seller**, or a **car broker**, Drive AI helps you understand the fair market value of a vehicle without depending on a middleman.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔵 **Used Car Price Prediction** | Predicts price based on company, model, year, fuel type, and kilometers driven |
| 🟢 **New Car Price Prediction** | Predicts price based on company, model, year, suspension type, and fuel type |
| 🟡 **Imported Car Price Prediction** | Predicts price based on company, model, year, fuel type, and kilometers driven |
| ⭐ **Car Reviews** | Users can submit reviews and ratings for cars they have owned |
| 📊 **Market Analytics (Power BI)** | Interactive dashboard showing sales trends, top performers, regional maps, forecasting, and key influencers |
| 🔐 **User Authentication** | Login system with PostgreSQL-backed user accounts via SQLAlchemy |

---

## 🖥️ Web Pages

| Page | Purpose |
|---|---|
| **Home** | Landing page with navigation to all three prediction modules |
| **Used Cars** | Input form → ML prediction for used vehicles |
| **Imported Cars** | Input form → ML prediction for imported vehicles |
| **New Cars** | Input form → ML prediction for brand new vehicles |
| **Reviews** | Community page for submitting car reviews and ratings |
| **Report** | Embedded Power BI dashboard for market trend analysis |
| **Help** | Help and FAQ page for user guidance |

---

## 🤖 Machine Learning Models

Three separate Linear Regression models are trained, one for each car type, and deployed via Flask using Pickle.

### 🔵 Used Car Model

| Detail | Info |
|---|---|
| **Dataset Source** | Kaggle (OLX + PakWheels combined) |
| **Dataset Size** | 2,250 records |
| **Input Features** | Car name, company, year, fuel type, kilometers driven |
| **Output** | Predicted price (PKR) |
| **Algorithm** | Linear Regression |
| **Test Accuracy** | **88%** |

**Key Correlations Found:**
- Older cars have significantly lower prices
- Diesel cars have the highest average price; LPG cars the lowest

---

### 🟢 New Car Model

| Detail | Info |
|---|---|
| **Dataset Source** | Pak Suzuki, Indus Toyota, and other official manufacturer websites |
| **Dataset Size** | 150 records |
| **Input Features** | Car name, company, year, suspension type, fuel type |
| **Output** | Predicted price (PKR) |
| **Algorithm** | Linear Regression |
| **Test Accuracy** | **98%** |

**Key Correlations Found:**
- Automatic suspension cars have the highest prices
- Toyota is the most expensive brand; Proton is the most affordable

---

### 🟡 Imported Car Model

| Detail | Info |
|---|---|
| **Dataset Source** | GitHub |
| **Dataset Size** | 650 records |
| **Input Features** | Car name, company, year, fuel type, kilometers driven |
| **Output** | Predicted price (PKR) |
| **Algorithm** | Linear Regression |
| **Test Accuracy** | **78%** |

**Key Correlations Found:**
- More kilometers driven = lower price
- Newer model years consistently have higher prices

---

## 🛠️ Tech Stack

### Machine Learning & Data
| Tool | Purpose |
|---|---|
| `Python` | Core ML development language |
| `scikit-learn` | Linear Regression model training |
| `pandas` | Data loading, cleaning, and manipulation |
| `numpy` | Numerical operations |
| `seaborn / matplotlib` | EDA and correlation visualizations |
| `pickle` | Serializing and saving trained ML models |
| `Jupyter Notebook` | Model development environment |

### Backend
| Tool | Purpose |
|---|---|
| `Flask` | Web framework and API routing |
| `flask-cors` | Handling cross-origin requests |
| `SQLAlchemy` | ORM for user authentication database |
| `PostgreSQL` | Database for storing user accounts and reviews |
| `PyCharm` | Backend development IDE |

### Frontend
| Tool | Purpose |
|---|---|
| `HTML / CSS` | Page structure and styling |
| `JavaScript` | Frontend interactivity |
| `Bootstrap` | Responsive UI components |
| `VS Code` | Frontend development IDE |

### Analytics
| Tool | Purpose |
|---|---|
| `Power BI` | Interactive market analytics dashboard |

---

## 📁 Project Structure

```
drive-ai/
│
├── app.py                          # Flask backend — routes and prediction logic
├── LinearRegressionModel321.pkl    # Trained model for Used Cars
├── LinearRegressionModel333.pkl    # Trained model for New Cars
├── LinearRegressionModel_imp.pkl   # Trained model for Imported Cars
│
├── datasets/
│   ├── Book111.csv                 # Used Car dataset
│   ├── Book11.csv                  # Imported Car dataset
│   └── newbook11.csv               # New Car dataset
│
├── notebooks/
│   ├── used_car_model.ipynb        # Used Car EDA and model training
│   ├── new_car_model.ipynb         # New Car EDA and model training
│   └── imported_car_model.ipynb    # Imported Car EDA and model training
│
├── templates/
│   ├── index.html                  # Home page
│   ├── login.html                  # Login page
│   ├── used_car.html               # Used Car prediction page
│   ├── new_car.html                # New Car prediction page
│   ├── imported_car.html           # Imported Car prediction page
│   ├── reviews.html                # Car reviews page
│   ├── report.html                 # Power BI analytics page
│   └── help.html                   # Help page
│
├── static/
│   ├── css/                        # Stylesheets
│   ├── js/                         # JavaScript files
│   └── images/                     # Background and UI images
│
└── README.md
```

---

## ⚙️ How to Run Locally

### Prerequisites
- Python 3.8+
- PostgreSQL installed and running
- pip

### Step 1 — Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/drive-ai.git
cd drive-ai
```

### Step 2 — Install dependencies
```bash
pip install flask flask-cors scikit-learn pandas numpy sqlalchemy psycopg2
```

### Step 3 — Set up the database
Make sure PostgreSQL is running. Update the database URI in `app.py`:
```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://postgres:yourpassword@localhost/ml-app'
```
Then run the app once to auto-create tables:
```bash
python app.py
```

### Step 4 — Open the app
Navigate to `http://localhost:5000` in your browser.

---

## 📊 How Prediction Works

1. User selects car details from the input form (company, model, year, fuel type, etc.)
2. Form data is sent via POST request to the Flask backend
3. Flask loads the relevant `.pkl` model using `pickle`
4. Input is structured as a pandas DataFrame and passed to `model.predict()`
5. Predicted price is returned and displayed on the page

```python
# Example prediction flow (Used Car)
prediction = model.predict(
    pd.DataFrame(
        columns=['name', 'company', 'year', 'kms_driven', 'fuel_type'],
        data=np.array([car_model, company, year, driven, fuel_type]).reshape(1, 5)
    )
)
return str(np.round(prediction[0], 2))
```

---

## 📈 Power BI Analytics Dashboard

The **Report** section features a 5-tab Power BI dashboard embedded in the web app:

| Tab | What It Shows |
|---|---|
| **Trends** | Sales trends, average price (4.96M PKR), average mileage (65.32K km), fuel type distribution |
| **Top Performers** | Top companies by sales (Toyota 12.55K, Suzuki 10.79K, Honda 9.28K), model counts, transmission breakdown |
| **Map** | City-wise sales distribution across Pakistan (Karachi, Lahore, Islamabad, etc.) with Q&A feature |
| **Forecasting** | Dollar rate forecasting and car sales volume predictions up to 2025 |
| **Key Influencers** | Factors that most increase car price (color, engine size, transmission type, assembly type) |

---

## 📋 Model Results Summary

| Model | Accuracy | Sample Prediction |
|---|---|---|
| Used Car | 88% | Toyota Aygo 2018, Diesel, 20,000 km → **RS 2,462,688.65** |
| Imported Car | 78% | Audi A3 Cabriolet 2019, Diesel, 21,412 km → **RS 2,568,382.45** |
| New Car | 98% | Honda Accord Turbo 2022, Manual, Petrol → **RS 9,074,006.94** |

---

## 🔮 Future Work

- Extend predictions to **motorcycles, trucks, and buses**
- Evolve into a **full car buying/selling marketplace** (similar to PakWheels/CarFirst)
- Add **AI chatbot** for customer support and recommendations
- Integrate **news feed and blogs** for automotive market updates
- Add **price filters** using ML instead of fixed price ranges

---

## 👥 Team

| Name | Seat No |
|---|---|
| **Muhammad Usman** | **B-191021**** |
| Muhammad Sameer Siddiqui | B-191020** |
| Mirza Viraad Baig | B-191020** |
| Umair Iqbal | B-191021** |


**Project Advisor:** Dr. Muhammad Saeed  
**Department:** Computer Science — University of Karachi  


---

## 📚 References

1. Pudaruth, S. (2014). *Predicting the Price of Used Cars Using Machine Learning Techniques*. International Journal of Information & Computation Technology, 4(7), 753–764.
2. Listiani, M. (2009). *Support Vector Regression Analysis for Price Prediction in a Car Leasing Application*. Master Thesis, Hamburg University of Technology.
3. [Towards Data Science — Car Price Prediction](https://towardsdatascience.com/predicting-car-price-using-machine-learning)
4. [Analytics Vidhya — ML vs Deep Learning for Car Prices](https://www.analyticsvidhya.com/blog/2021/07/car-price-prediction-machine-learning-vs-deep-learning/)
