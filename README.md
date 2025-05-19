import pandas as pd
# Load data
sales = pd.read_csv("sales_data.csv")
stores = pd.read_csv("store_info.csv")

# Tambah kolom total price
sales['total_price'] = sales['quantity'] * sales['price'] * (1 - sales['discount'])

# Total penjualan per produk
print(sales.groupby('product')['total_price'].sum())

# Merge dengan store_info
merged = pd.merge(sales, stores, on='store_id')

# Visualisasi penjualan per kategori
import seaborn as sns
import matplotlib.pyplot as plt
sns.barplot(x='category', y='total_price', data=sales)
plt.show()
