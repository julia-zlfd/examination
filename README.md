# examination
# Koordinater är →  lat: 59.30996552541549
#                   lon: 18.02151508449004
#                   d.v.s. STI Liljeholmen

from typing import Any
import requests


def fetch_data_from_smhi() -> Any:
    print("Ladda ner senaste data från SMHI")
    url = "https://opendata-download-metfcst.smhi.se/api/category/pmp3g/version/2/geotype/point/lon/18.0215/lat/59.3099/data.json"
    data = requests.api.get(url).json()
    return data

def fetch_data_from_owm() -> Any:
    print("Ladda ner senaste data från OpenWeatherMap")
    url = "https://api.openweathermap.org/data/3.0/onecall?lat=59.3099&lon=18.0215&exclude=current,minutely,daily,alerts&appid={API key}"
    data = requests.api.get(url).json()
    return data

def store_data_in_excel(data: Any, provider: str) -> None:
    print(f"Store in Excel the data {data} from {provider} provider")


def print_report() -> None:
    print(f"Prognos från SMHI <datum>:")

while True:
    print("MENY")
    print("----")
    print("1. Hämta senaste data")
    print("2. Skriv ut prognos")
    print("9. Avsluta")
    print()

    choice = input("Ange ditt val: ")

    if choice == '1':
        print()
        print("Du valde 'Hämta senaste data'")
        print()
        
        while True:
            print("Provider")
            print("--------")
            print("1. SMHI")
            print("2. OpenWeatherMap")
            print("3. Båda")
            print("9. Gå tillbaka till meny")
            print()

            choice_provider = input("Välj provider: ")

            if choice_provider == '1':
                print()
                print("Du valde 'Ladda ner senaste data från SMHI'")
                print()
                data = fetch_data_from_smhi()
                store_data_in_excel(data, 'SMHI')
                print()
            elif choice_provider == '2':
                print()
                print("Du valde 'Ladda ner senaste data från OpenWeatherMap'")
                print()
                data = fetch_data_from_owm()
                store_data_in_excel(data, 'OpenWeatherMap')
                print()
            elif choice_provider == '3':
                print()
                print("Du valde 'Ladda ner senaste data från båda'")
                print()
                data = fetch_data_from_smhi()
                store_data_in_excel(data, 'SMHI')
                data = fetch_data_from_owm()
                store_data_in_excel(data, 'OpenWeatherMap')
                print()
            elif choice_provider == '9':
                print()
                print("Du valde 'Gå tillbaka till meny'")
                print()
                break # this is to break the while loop and go back to menu
            else:
                print()
                print("Ogiltigt val. Var god försök igen.")
                print()
    elif choice == '2':
        print()
        print("Du valde 'Skriv ut prognos'")
        print()
        print_report()
        print()
    elif choice == '9':
        print()
        print("Avslutar programmet. Adjö!")
        print()
        break  # this is to break the while loop and exit
    else:
        print()
        print("Ogiltigt val. Var god försök igen.")
        print()
