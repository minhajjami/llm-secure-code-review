# Day 1 — OWASP Benchmark

## What is the OWASP Benchmark?

The OWASP Benchmark is a standardized test suite for evaluating the accuracy and effectiveness of automated application-security vulnerability detection tools. It provides test cases with known security outcomes, allowing the results produced by a detection tool to be compared against ground truth.

## What is a CWE?

CWE (Common Weakness Enumeration) is a standardized taxonomy of software and hardware weaknesses. It provides identifiers and descriptions for recurring classes of security weaknesses, such as SQL Injection, Buffer Overflow, and Path Traversal.

## What is a vulnerable test case?

A vulnerable test case contains code intentionally constructed to represent a known security vulnerability. The associated ground truth identifies the relevant weakness, such as a CWE category.

For example:

Source code → user-controlled input → SQL query → SQL Injection → CWE-89

## What is a safe test case?

A safe test case represents code that does not contain the targeted vulnerability and therefore should not be flagged as vulnerable by a detection tool.

## How is a detection result evaluated?

The tool's prediction is compared with the known ground truth.

| Ground Truth | Prediction | Result         |
| ------------ | ---------- | -------------- |
| Vulnerable   | Vulnerable | True Positive  |
| Vulnerable   | Safe       | False Negative |
| Safe         | Vulnerable | False Positive |
| Safe         | Safe       | True Negative  |

These outcomes allow us to calculate metrics such as precision, recall, and F1-score.

## What information is available for each test case?

Each Benchmark test case includes source code and associated benchmark information/metadata. We will inspect the actual benchmark files before deciding which information should be used as LLM input and which information must remain ground truth for evaluation.

This distinction is important because giving the LLM ground-truth vulnerability information would introduce data leakage into our experiment.

## Initial CWE categories

We initially plan to investigate:

* CWE-89 — SQL Injection
* CWE-78 — OS Command Injection
* CWE-22 — Path Traversal
* CWE-79 — Cross-Site Scripting

## Why is the OWASP Benchmark appropriate?

The Benchmark provides known ground truth for vulnerability cases, making it possible to evaluate LLM predictions quantitatively.

It allows us to compare:

LLM prediction → Ground truth → TP / TN / FP / FN

This is particularly useful for our research question because we want to determine whether additional static-analysis context improves vulnerability detection rather than simply measuring how many vulnerabilities an LLM can identify.
