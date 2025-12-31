import streamlit as st
import yfinance as yf
import pandas as pd

# Page setup
st.set_page_config(page_title="Safer Double Radar", layout="wide")
st.title("📈 Safer Double Radar — Mid-Cap Double Candidates")
st.caption("Safer double probability based on volume, momentum, and consolidation")

# List of slightly safer mid-cap stocks
TICKERS = [
    "AAPL","MSFT","NVDA","AMD","PLTR",
    "SOFI","NFLX","META","COIN","UPST",
    "RBLX","SNAP","DOCU","LCID","RIVN"
]

# Function to calculate Double Probability Score (DPS)
def scan_stock(ticker):
    stock = yf.Ticker(ticker)
    hist = stock.history(period="14d")  # last 2 weeks for stability

    if hist.empty or len(hist) < 3:
        return None

    price = hist["Close"][-1]
    price_range = (hist["High"].max() - hist["Low"].min()) / price
    compression_score = max(0, 1 - price_range)  # sideways = good

    volume_spike = hist["Volume"][-1] / hist["Volume"].mean()  # current vs avg
    momentum = (hist["Close"][-1] - hist["Close"][-3]) / hist["Close"][-3]  # short-term

    # DPS formula (tuned for safer
