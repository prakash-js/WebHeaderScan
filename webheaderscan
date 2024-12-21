import requests
import os
from colorama import Fore , init
from requests.exceptions import *

def main(wordlists):
    with open('output.txt', 'aw') as output:
        output.write("\n"+"\n" + "_____________________________________________________________________________" + "\n"+"\n")
        with open(wordlists, 'r') as payload:
            for check in payload:
                check_status = url + check.strip()
                try:
                    response = requests.get(check_status)
                    status_code = response.status_code
                    if status_code == 200 or status_code == 302 or status_code == 500 or status_code == 405:
                        print(f"{check_status} [{response.status_code}]")
                        output.write(check_status + "\n")
                except requests.exceptions:
                    pass




if __name__ == '__main__':

    init(autoreset=True)

    while True:
        url_list = str(input("Enter the url file : "))
        if os.path.exists(url_list):
            break
        else:
            print("File Not Found")

    with (open(url_list, 'r') as reading):
        for url in reading:
            url = url.strip()
            try:
                if url[-1] != '/':
                    url += '/'
            except IndexError:
                pass
            try:
                response_2 = requests.get(url)
                power_by = response_2.headers.get('X-Powered-By', 'unknown')
                server = response_2.headers.get('Server', 'unknown')
            except RequestException as e:
                print(f"ERROR in URL{url}")



            server_list = ['Apache','Tomcat', 'IIS', 'nginx']
            power_list = ['PHP', 'Express']

            for i in server_list:
                if i in server:
                    print(f" web server  : {url} {Fore.RED}[{server}]")
                    wordlist = f"payloads/{i}.txt"
                    main(wordlist)
                elif server == 'unknown':
                    print(f"Can't find the server name in Header")
                else:
                    print(f"{Fore.YELLOW}{url} : New Server name found : {server}")


            for j in power_list:
                if j in power_by:
                    print(f" site power by : {url} {Fore.RED}[{power_by}]")
                    wordlist = f"payloads/{j}.txt"
                    main(wordlist)
                elif power_by == 'unknown':
                    print(f"Can't find the power-by Header")
                else:
                    print(f"{Fore.YELLOW}{url} : New x-power-by name found : {server}")



