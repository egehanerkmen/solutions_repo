

# Problem 1

# 📊 Exploring the Central Limit Theorem through Simulations

## 🎯 Objective

To understand how the **Central Limit Theorem (CLT)** works in practice by simulating sampling distributions from different population distributions.

---

## 1️⃣ Defining Population Distributions

We begin by generating large synthetic populations using three distinct probability distributions:

### 📌 Selected Distributions:

- **Uniform Distribution**$U(a,b)$

- **Exponential Distribution**$\text{Exp}(\lambda)$

- **Binomial Distribution**$\text{Bin}(n,p)$

### 🧮 Mathematical Definitions:

- **Uniform Distribution**:
  
$$
f(x)=\frac{1}{b-a},\quad x\in[a,b]
$$

- **Exponential Distribution**:
  
$$
f(x)=\lambda e^{-\lambda x},\quad x\geq0
$$

- **Binomial Distribution**:
  
$$
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k},\quad k=0,1,\dots,n
$$

### 🧪 Visuals for Populations:

![image](https://github.com/user-attachments/assets/de3b1c61-5a8d-493b-8e2d-e4fe6cc3aacb)
--

## 3️⃣ Creating Sampling Distributions

To observe the Central Limit Theorem (CLT) in action, we construct **sampling distributions of the sample mean**.

### 🔁 Procedure

- For each selected sample size $n \in \{5,10,30,50\}$:

- Randomly draw $n$ values from the population **with replacement** (or without, if the population is large).

- Calculate the sample mean $\bar{x}$.

- Repeat this process $M=1000$ times to form a **sampling distribution of the mean**.

### 🧮 Formula for Sample Mean

For a sample of size $n$ with observations $x_1,x_2,\dots,x_n$, the sample mean is given by:

$$
\bar{x}=\frac{1}{n}\sum_{i=1}^{n}x_i
$$

### 🧪 Visuals for Sampling Distributions

![image](https://github.com/user-attachments/assets/615d21fa-106b-4163-b379-0e3f13c6649d)
--
![image](https://github.com/user-attachments/assets/c13d862b-7dd2-43c9-a40c-2a58b383b6e5)
--
![image](https://github.com/user-attachments/assets/1f2d75b3-3299-4776-9c2f-3c49628489c7)
--


## 5️⃣ Exploring Parameters of the Central Limit Theorem

This section examines how different **parameters** influence the behavior of the sampling distributions.

---

### 🔍 Key Questions:

- How does the **shape** of the original distribution affect convergence?
- How does the **sample size** influence the approach to normality?
- How does the **population variance** affect the **spread** of the sampling distribution?

---

### 🧠 Theoretical Expectations:

#### 📌 Original Distribution Shape

- The CLT states that the sampling distribution of the mean $\bar{x}$ 
approaches a **normal distribution** regardless of the population’s shape, provided that:

- The sample size is **sufficiently large**.

- The population has **finite mean and variance**.

#### 📌 Sample Size and Normality

- Larger sample sizes $n$ cause:

- Smoother and more symmetric sampling distributions.
- Faster convergence toward the **normal distribution**.

- **Rule of thumb**:

- $n \geq 30$ is often enough for skewed distributions.

#### 📌 Population Variance and Spread

- The variance of the sampling distribution is:

$$
\sigma_{\bar{x}}^2 = \frac{\sigma^2}{n}
$$

- As sample size $n$ increases:

- The **standard error** decreases.

- The **spread** of the sampling distribution becomes **narrower**.

---

### 🧪 Empirical Observations from Simulation

- **Uniform** distribution converges rapidly — already bell-shaped at $n=10$.

- **Exponential** distribution (skewed) requires larger $n$ to become symmetric.

- **Binomial** distribution shows quick convergence for $n \geq 30$ due to its discrete nature.

---

## 6️⃣ Drawing Practical Conclusions

The Central Limit Theorem has **powerful real-world applications**, especially when working with **sample statistics**.

---

### 🛠 Applications in Practice

- **📏 Estimation Techniques**:
- Enables constructing **confidence intervals** for unknown population means:
  
$$
\bar{x} \pm z^* \cdot \frac{\sigma}{\sqrt{n}}
$$

- **🏭 Quality Assurance**:

- Detecting shifts in production processes using sample means.

- Central to **control charts** and **Six Sigma** methods.

- **💸 Financial Predictions**:
- Estimating returns on portfolios.
- Risk analysis based on sampling distributions of historical data.

---

### ✅ Summary Points

- The **CLT bridges the gap** between unknown population distributions and practical inferential tools.

- Even with **non-normal** populations, we can make reliable predictions using the **sample mean**.

- Understanding how **sample size and variance** affect results is essential for **sound statistical practice**.

---











