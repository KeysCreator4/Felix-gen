import requests
import json
import time

url = "https://api.discord.gx.games/v1/direct-fulfillment"
headers = {
    "authority": "api.discord.gx.games",
    "method": "POST",
    "path": "/v1/direct-fulfillment",
    "scheme": "https",
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate, br",
    "Accept-Language": "en-US,en;q=0.9",
    "Content-Type": "application/json",
    "Origin": "https://www.opera.com",
    "Referer": "https://www.opera.com/",
    "Sec-Ch-Ua": '"Chromium";v="116", "Not)A;Brand";v="24", "Opera GX";v="102"',
    "Sec-Ch-Ua-Mobile": "?0",
    "Sec-Ch-Ua-Platform": '"Windows"',
    "Sec-Fetch-Dest": "empty",
    "Sec-Fetch-Mode": "cors",
    "Sec-Fetch-Site": "cross-site",
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36 OPR/102.0.0.0 (Edition std-1)"
}

payload = {
    "partnerUserId": "1"
}

file_path = "e.txt"
base_url = "https://discord.com/billing/partner-promotions/1180231712274387115/"

def make_request():
    try:
        response = requests.post(url, headers=headers, json=payload)
        response.raise_for_status()
        response_json = response.json()
        token = response_json.get("token", "")
        if token:
            full_url = base_url + token
            with open(file_path, "a") as file:
                file.write(full_url + '\n')
            print(f"URL saved: {full_url}")
        else:
            print("Token not found in the response.")
    except requests.exceptions.HTTPError as errh:
        print(f"HTTP Error: {errh}")
    except requests.exceptions.RequestException as err:
        print(f"Request Error: {err}")
    except Exception as e:
        print(f"Error: {e}")

if __name__ == "__main__":
    while True:
        make_request()
        time.sleep(0.1)
