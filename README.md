# Fully Homomorphic Encryption Studio

[FHE-Studio.com](https://fhe-studio.com) is an open source IDE for anyone who want to create programs that process encrypted data.

# What is Homomorphic Encryption

Homomorphic encryption is a cryptographic technique that allows you to perform operations on encrypted data without needing to decrypt it first. This is valuable in situations where privacy and security are paramount, such as in cloud computing or data outsourcing scenarios.

Imagine you have some sensitive data, like your salary, stored in an encrypted form. Traditional encryption would require you to decrypt it first to perform any calculations or operations. But with homomorphic encryption, you can perform mathematical operations on the encrypted data itself, and the result will also be encrypted.

For example, if your encrypted salary is represented as "X" and you want to calculate your taxes by multiplying it by a tax rate, you can do that without ever revealing the actual salary or tax rate. You'll get an encrypted result, let's call it "Y," which only you or authorized parties can decrypt to obtain the final tax amount.

So, in a nutshell, homomorphic encryption is like having a secure mathematical superpower that lets you manipulate encrypted data without exposing the sensitive information it contains. It's an essential tool for protecting data privacy in various applications, including secure computation and data analytics.

[More on FHE Business value](why-fhe.md)


# FHE program

## 1. Choose From A List of Available Circuits
![Alt text](misc/fhe-studio-1.png "List of Circuits")
## 2. Or Program a Circuit Yourself
![Alt text](misc/fhe-studio-2.png "Program a Circuit")
## 3. Add a Program to Key Vault to Encrypt, Run, Decrypt!
![Alt text](misc/fhe-studio-3.png "Evaluation Vault")

# How to build FHE programs

[Open the development guide](how-to-build-fhe-circuits.md)



