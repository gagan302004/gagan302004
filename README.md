import matplotlib.pyplot as plt
from matplotlib.dates import DateFormatter, WeekdayLocator, DayLocator
from mplfinance.original_flavor import candlestick_ohlc
import pandas as pd
import numpy as np
import datetime

# Sample data
data = {'Date': [datetime.date(2023, 1, 1), datetime.date(2023, 1, 2), datetime.date(2023, 1, 3), datetime.date(2023, 1, 4)],
        'Open': [100, 110, 105, 115],
        'High': [120, 125, 115, 118],
        'Low': [95, 105, 100, 112],
        'Close': [115, 120, 110, 114]}
df = pd.DataFrame(data)

# Convert dates to Matplotlib date format
df['Date'] = pd.to_datetime(df['Date'])
df['Date'] = df['Date'].apply(lambda x: matplotlib.dates.date2num(x))

# Create a new figure
fig, ax = plt.subplots()

# Plot candlestick chart
candlestick_ohlc(ax, zip(df['Date'], df['Open'], df['High'], df['Low'], df['Close']), width=0.6)

# Formatting
ax.xaxis.set_major_formatter(DateFormatter('%Y-%m-%d'))
ax.xaxis.set_major_locator(WeekdayLocator())
ax.xaxis.set_minor_locator(DayLocator())
plt.xticks(rotation=45)
plt.xlabel('Date')
plt.ylabel('Price')
plt.title('Candlestick Chart')
plt.grid(True)

plt.show()
