# A real-time crypto price tracker that alerts you when a target price is reached.
import requests
import time

def get_crypto_price(ticker="bitcoin"):
    url = f"https://api.coingecko.com/api/v3/simple/price?ids={ticker}&vs_currencies=usd"
    response = requests.get(url).json()
    return response[ticker]["usd"]

def monitor_price(ticker, target):
    print(f"🚀 Monitoring {ticker}... Target: ${target}")
    while True:
        current_price = get_crypto_price(ticker)
        if current_price >= target:
            print(f"🔔 ALERT! {ticker.upper()} reached ${current_price}")
            break
        print(f"📉 {ticker.upper()} is currently at ${current_price}. Retrying...")
        time.sleep(30)

if __name__ == "__main__":
    monitor_price("bitcoin", 70000)
