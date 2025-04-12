import pandas as pd
import matplotlib.pyplot as plt

# Manually preparing the cleaned dataset from user's structured input
data = {
    "T": list(range(1, 32)),
    "FC": [2, 11, 2, 4, 3, 1, 1, 2, 4, 0, 4, 1, 3, 0, 1, 1, 2, 1, 8, 9, 6, 7, 4, 3, 0, 4, 1, 0, 2, 2, 3],
    "E": [0.05, 1, 0.19, 0.41, 0.32, 0.61, 0.32, 1.83, 3.01, 1.79, 3.17, 3.4, 4.2, 1.2, 0.0531, 0.0619, 0.158, 0.081,
          1.046, 1.75, 2.96, 4.97, 0.42, 4.7, 0.9, 1.5, 2, 1.2, 1.2, 2.2, 7.6]
}

df = pd.DataFrame(data)

# Compute cumulative failure count and cumulative time for RDC
df["Cumulative FC"] = df["FC"].cumsum()
df["Cumulative Time"] = df["E"].cumsum()

print(df[["T", "Cumulative FC", "Cumulative Time"]].head(10) ) # Show first 10 rows for validation
