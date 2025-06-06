# Adversarial Attacks on Neural Networks 🛡️

This repository contains code and experiments evaluating adversarial attacks and defenses on CNN models trained on CIFAR‑10. The goal was to build robust image classifiers through **Min-Max adversarial training**.

---

## 📁 Repository Structure

```
.
├── notebooks/
│   ├── `CIFAR (3).ipynb`          # Baseline CNN for CIFAR-10
│   └── `Adversarial_attck (1).ipynb` # FGSM evaluation & Min-Max robust training
├── data/                         # Scripts/notebooks to download or preprocess CIFAR-10
├── src/
│   ├── `model.py`                # CNN architecture definition
│   ├── `train_baseline.py`       # Code to train baseline CNN
│   ├── `fgsm_attack.py`          # FGSM attack implementation
│   └── `train_robust.py`         # Min-Max adversarial training routine
├── images/                       # Figures for accuracy curves, confusion matrices, etc.
│   ├── `confusion_matrix_baseline.png`
│   ├── `accuracy_vs_epsilon_baseline.png`
│   └── `…`
├── requirements.txt              # Python dependencies
└── README.md                     # This file
```

---

## 🎯 Objectives & Results

- **Baseline CNN** achieved **78.6%** accuracy on clean CIFAR-10.
- Under FGSM perturbations:
  - With ε = 0.001 ➝ accuracy dropped to ~43.3%
  - With ε = 0.01 ➝ accuracy dropped to ~2.3%
- **Robust model** trained using Min-Max adversarial training:
  - Clean accuracy: **69.3%**
  - ε = 0.001 ➝ **55.2%**, ε = 0.01 ➝ **4.7%**

📈 These results highlight the effectiveness of adversarial training—while clean accuracy slightly decreases, robustness against attacks improves significantly.

---

## 🚀 Installation

1. **Clone the repo:**
   ```bash
   git clone https://github.com/anirudhksharma/Adverseral_Attacks_on_Neural_Net.git
   cd Adverseral_Attacks_on_Neural_Net
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Download CIFAR-10 data:**  
   Use the notebook in `notebooks/` or modify scripts in `data/`.

---

## 🔧 Usage

- **Train baseline model:**
  ```bash
  python src/train_baseline.py
  ```

- **Evaluate FGSM attack on baseline:**
  ```bash
  python src/fgsm_attack.py --model baseline
  ```

- **Train robust model with Min-Max FGSM:**
  ```bash
  python src/train_robust.py --epsilon 0.001
  ```

- **Evaluate robust model under attack:**
  ```bash
  python src/fgsm_attack.py --model robust --epsilon 0.001
  ```

---

## 📚 Background

The **FGSM** attack (Goodfellow et al., 2015) perturbs inputs via:
```
x_adv = x + ε · sign(∇_x L(f(x), y))
```
**Min-Max adversarial training** seeks to solve:
\[
\min_θ \, E_{x,y}\left[\max_{\|δ\|≤ε} L(f_θ(x+δ),y)
ight]
\]
This approach improves resilience against perturbations.

### Other common defense methods:
- Defensive Distillation
- Gradient Masking
- Randomized Smoothing

🧠 Read more in `Comparison with Other Defense Methods` section in the main report.

---

## 📖 References

- Goodfellow, I. J., Shlens, J., & Szegedy, C. (2015). *Explaining and Harnessing Adversarial Examples*. arXiv:1412.6572
- Madry, A., et al. (2018). *Towards Deep Learning Models Resistant to Adversarial Attacks*. arXiv:1706.06083
- Papernot, N., et al. (2017). *Ensemble Adversarial Training: Attacks and Defenses*. arXiv:1705.07204

---

## 📝 License

This work is licensed under the MIT License. See [LICENSE](LICENSE) for details.

