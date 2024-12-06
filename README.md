# 🎲 Lotto Simulator Web Application

This project is a web-based lottery simulator designed for research purposes. The goal is to showcase how many attempts it takes to achieve specific matches, up to a jackpot (5 hits). The simulation replicates the Hungarian *Ötös Lottó* mechanics.

---

## 📝 Application Specification

### 🎯 Key Features:
1. **Automated Simulation**:  
   - The simulation starts automatically when the page loads and runs continuously.
   - Stops when a 5-hit ticket is achieved, highlighting the elapsed years prominently.

2. **Lotto Mechanics**:  
   - Generates 5 numbers from 1 to 90, without repetition.
   - Displays the drawn numbers on the interface.

3. **Player Interaction**:  
   - Players can choose their own numbers or play with random selections.  
   - Input fields or pre-defined numbers are acceptable for user selection.

4. **Adjustable Speed**:  
   - A slider allows users to control the draw speed, ranging from 1 second to 1 millisecond.

5. **Progress Indicators**:  
   - Displays the total duration of play in years (*1 draw per week*).  
   - Shows the number of tickets submitted and counts for 2, 3, 4, and 5-hit results.  
   - Tracks the total money spent on tickets (*300 HUF per ticket*).

---

## 🔧 Technical Details

### 💻 Frontend Requirements:
- **Framework**: Use any modern front-end framework (Vue.js is optional).  
- **Styling**: Preferably use SASS for styling, but any modern preprocessor is acceptable.  

### ✨ Extra Features (for bonus points):
- Use a more reliable number generation algorithm than `Math.random` (e.g., Crypto API).  
- Deploy the application using a CI/CD pipeline.  
- Ensure the app is responsive and mobile-friendly.

### 🛠 Development Practices:
- Use Git for version control.
- Provide a public repository link or include the Git history.

---

## 🚀 How It Works

1. **Simulation Start**: Automatically begins on page load.
2. **Gameplay Options**:
   - Select custom numbers or generate random ones.
3. **Track Progress**:
   - Monitor matches, elapsed time, tickets bought, and total expenses.
4. **Adjust Speed**:
   - Use the slider to change the draw speed dynamically.

---

## 🎨 User Interface Design

- **Responsive Design**: Works seamlessly on desktop and mobile devices.
- **Highlighting Jackpot**: The simulation pauses and highlights when a 5-hit is achieved.
- **Intuitive Controls**: Simple controls for number selection and speed adjustment.

---

## 🔗 Repository

[GitHub Repository](#) *(Replace with your actual repo link)*

---

## ⚙️ Technical Highlights

- **Random Number Generation**:  
  Utilizes a reliable method (e.g., Crypto API) for number generation.

- **Responsive and Modern Design**:  
  Built with a mobile-first approach for optimal user experience.

- **Deployment**:  
  Supports deployment via CI/CD pipelines.

---

## 🖥️ Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/lotto-simulator.git
   cd lotto-simulator
