# Fully Homomorphic Encryption Studio

[FHE-Studio.com](https://fhe-studio.com) is an open source IDE for anyone who want to create programs that process encrypted data.

# What is Homomorphic Encryption

Homomorphic encryption is a cryptographic technique that allows you to perform operations on encrypted data without needing to decrypt it first. This is valuable in situations where privacy and security are paramount, such as in cloud computing or data outsourcing scenarios.

Imagine you have some sensitive data, like your salary, stored in an encrypted form. Traditional encryption would require you to decrypt it first to perform any calculations or operations. But with homomorphic encryption, you can perform mathematical operations on the encrypted data itself, and the result will also be encrypted.

For example, if your encrypted salary is represented as "X" and you want to calculate your taxes by multiplying it by a tax rate, you can do that without ever revealing the actual salary or tax rate. You'll get an encrypted result, let's call it "Y," which only you or authorized parties can decrypt to obtain the final tax amount.

So, in a nutshell, homomorphic encryption is like having a secure mathematical superpower that lets you manipulate encrypted data without exposing the sensitive information it contains. It's an essential tool for protecting data privacy in various applications, including secure computation and data analytics.

[More on FHE Business value](why-fhe.md)

# FHE Studio
The objective of this project is to create a user-friendly, open-source IDE specifically tailored for fully homomorphic encryption (FHE) development. FHE is a groundbreaking technology with immense potential to protect sensitive data while still allowing for computation on encrypted data. Existing encryption methods, like AES and RSA, protect data at rest and in transit, but the data must be decrypted for processing. This exposes it to potential breaches and insider threats during the processing stage. FHE stays always encrypted while processing, decrypting the final result(s) only.

FHE-Studio.com is a free open source IDE for anyone who wants to create programs that process encrypted data & AI models. FHE significantly simplifies the cyber security architecture. Unlike Zero Trust, which requires intricate security layers and policies, FHE integrates into public clouds with minimal disruption.

FHE is considered one of the most promising cryptographic technologies to address the security challenges posed by quantum computing, often referred to as the "post-quantum" era, which makes it a favourable cybersecurity choice for public data sharing (e.g. Blockchain)

However, it remains a complex and resource-intensive field. Therefore, an intuitive and accessible development environment is essential for advancing FHE applications and expanding its adoption.


# FHE program

## 1. Choose From A List of Available Circuits
![Alt text](misc/fhe-studio-1.png "List of Circuits")
## 2. Or Program a Circuit Yourself
![Alt text](misc/fhe-studio-2.png "Program a Circuit")
## 3. Add a Program to Key Vault to Encrypt, Run, Decrypt!
![Alt text](misc/fhe-studio-3.png "Evaluation Vault")

# How to build FHE programs

[Open the development guide](how-to-build-fhe-circuits.md)



