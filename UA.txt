import random
import argparse
import sys  # To use sys.exit()

# List of user agent templates
user_agents = [
    # Chrome User Agents
    "Mozilla/5.0 (Linux; Android {version}; {country}; {device}) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/{chrome_version} Mobile Safari/537.36",
    
    # Facebook App User Agents
    "Mozilla/5.0 (Linux; Android {version}; {country}; {device}) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/{chrome_version} Mobile Safari/537.36 [FB_IAB/FB4A;FBAV/{fb_version}]",
    
    # Facebook Lite User Agents
    "Mozilla/5.0 (Linux; Android {version}; {country}; {device}) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/{chrome_version} Mobile Safari/537.36 [FB_IAB/FBAN/FB_LITE;FBAV/{fb_version}]",
    
    # Katana User Agents
    "Mozilla/5.0 (Linux; Android {version}; {country}; {device}) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/{chrome_version} Mobile Safari/537.36 [FBAN/FB4A;FBAV/{katana_version}]"
]

# Random device and version pools
android_versions = ["6.0", "7.0", "8.1.0", "9", "10"]
devices = ["Samsung Galaxy S10", "OPPO A37f", "HUAWEI P30", "Xiaomi Redmi Note 8", "vivo 1901"]
chrome_versions = ["55.0.2883.91", "68.0.3440.91", "78.0.3904.108", "80.0.3987.132", "83.0.4103.106"]
fb_versions = ["178.0.0.35.82", "186.0.0.39.85", "203.0.0.30.99", "214.0.0.24.98", "257.0.0.28.105"]
katana_versions = ["150.0.0.32.102", "132.0.0.19.97", "206.0.0.35.99", "214.0.0.24.98"]

# Country options
countries = {
    'PH': 'en-PH',  # Philippines
    'US': 'en-US',  # United States
    'IN': 'en-IN',  # India
    'UK': 'en-GB',  # United Kingdom
    'FR': 'fr-FR',  # France
    'JP': 'ja-JP'   # Japan
}

# Generate random user agent
def generate_user_agent(country_code):
    template = random.choice(user_agents)
    return template.format(
        version=random.choice(android_versions),
        device=random.choice(devices),
        chrome_version=random.choice(chrome_versions),
        fb_version=random.choice(fb_versions),
        katana_version=random.choice(katana_versions),
        country=countries.get(country_code, 'en-US')  # Default to US if country code not found
    )

# Main script with argument parsing
if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Generate random user agents.")
    parser.add_argument("-c", "--country", help="Specify the country code (e.g., US, PH, IN)", default="US")
    parser.add_argument("-n", "--number", help="Specify the number of user agents to generate", type=int, default=100)
    
    args = parser.parse_args()

    country_code = args.country.upper()
    num_agents = args.number

    for _ in range(num_agents):
        print(generate_user_agent(country_code))
    
    # After generating, ask user if they want to exit
    while True:
        exit_choice = input("\nDo you want to exit the program? (yes/no): ").lower()
        if exit_choice == "yes":
            print("Exiting the program. Goodbye!")
            sys.exit()
        elif exit_choice == "no":
            print("Program will continue running.")
            break
        else:
            print("Invalid input. Please type 'yes' or 'no'.")