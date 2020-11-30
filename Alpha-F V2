#Importing Moduels To Use
import sys
import os
import os.path
import time
import random
import requests
import pymysql
import colorama
import ctypes

from random import randint
from colorama import Fore, init, Style
from requests import get
from update_check import isUpToDate
from update_check import update
#----------END----------

#Blank Space
bs = ('                        ')
#----------END----------

#Colors
RED = Fore.RED
BLUE = Fore.BLUE
BLACK = Fore.BLACK
CYAN = Fore.CYAN
MAGENTA = Fore.MAGENTA
WHITE = Fore.WHITE
YELLOW = Fore.YELLOW
GREEN = Fore.GREEN
#----------END----------

#Under Develompent
def development():
    logo()
    print(WHITE + "[" + YELLOW + "!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!" + WHITE + "]")
    print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> This section is currently under development.")
    print(WHITE + "[" + YELLOW + "!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!" + WHITE + "]")
    print()
    input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Press any key to continue")
#----------END----------

#Public IP
public_ip = get("https://api.ipify.org").text
#----------END----------

#Version Graber
version = "0.2a"
if isUpToDate(__file__, "https://raw.githubusercontent.com/username/repo/myProgram.py") == False:
   latest_version = WHITE + "[" + MAGENTA + version + WHITE + "]"
else:
    latest_version = WHITE + "[" + MAGENTA + "OLD" + WHITE + "]"
#----------END----------

#MySQL Database Connector
def mysql_check():
    try:
        global connection
        connection = pymysql.connect(host="sql2.freemysqlhosting.net", user="sql2377934", password="mT1%jT2!", db="sql2377934")
    except:
        print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Could not establish a connection to Database Server.")
        print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Maybe server is down?")
        print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Please report this error to an Admin or a Dev.")
        time.sleep(3)
        startup_menu()
#----------END----------

#Server Status Checker
def status_checker():
    try:
        global mysql_status
        mysql_check = pymysql.connect(host="sql2.freemysqlhosting.net", user="sql2377934", password="mT1%jT2!", db="sql2377934")
        mysql_status = GREEN + "Operational"
    except:
        mysql_status = RED + "Offline"
#----------END----------

#Alpha-F Logo
def logo():
    ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Main Menu")
    os.system('cls')
    print() 
    print(" █████  ██      ██████  ██   ██  █████       " + MAGENTA +" ███████ " + WHITE)
    print("██   ██ ██      ██   ██ ██   ██ ██   ██      " + MAGENTA +" ██      " + WHITE)
    print("███████ ██      ██████  ███████ ███████ █████" + MAGENTA +" █████   " + WHITE)
    print("██   ██ ██      ██      ██   ██ ██   ██      " + MAGENTA +" ██      " + WHITE)
    print("██   ██ ███████ ██      ██   ██ ██   ██      " + MAGENTA +" ██      " + WHITE)
    print("                                             " + latest_version)
    print(WHITE)
#----------END----------

#Startup Menu Screen
def startup_menu():
    ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Server Status")
    logo()
    print(WHITE + "[" + YELLOW + "Discord" + WHITE + "] https://discord.gg/stg9W55D")
    print()
    print(WHITE + "[" + MAGENTA + "1" + WHITE + "] Sign In")
    print(WHITE + "[" + MAGENTA + "2" + WHITE + "] Sign Up")
    print(WHITE + "[" + MAGENTA + "3" + WHITE + "] Server Status")
    print(WHITE + "[" + MAGENTA + "0" + WHITE + "] Exit")
    print()
    startup_menu_option = input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "]  >>> ")


    if startup_menu_option == "1":
        login()
        pass

    elif startup_menu_option == "2":
        register()
        pass

    elif startup_menu_option == "3":
        server_status()
        pass

    elif startup_menu_option == "0":
        exit()

    else:
        print()
        print(WHITE + "[" + MAGENTA + "MAGENTA-F" + WHITE + "] >>> Invalid command ")
        time.sleep(1)
        startup_menu()
#----------END----------

#Server Status Screen
def server_status():
    ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Server Status")
    status_checker()
    logo()
    print(WHITE + "[" + MAGENTA + "Database Server" + WHITE + "] >>> " + mysql_status)
    print()
    input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Press any key to continue")
    startup_menu()
#----------END----------

#Register Menu
def register():
    print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Connecting to server")
    ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Sign Up")
    logo()
    mysql_check()
    username_alphaf = input(WHITE + "[" + MAGENTA + "Username" + WHITE + "] >>> ")
    password_alphaf = input(WHITE + "[" + MAGENTA + "Password" + WHITE + "] >>> ")
    email_alphaf = input(WHITE + "[" + MAGENTA + "Email" + WHITE + "] >>> ")
    token_alphaf = input(WHITE + "[" + MAGENTA + "Token" + WHITE + "] >>> ")
    cur = connection.cursor()
    username_alphaf_lowercase = username_alphaf.lower()
    query = "SELECT * FROM alphaf_users WHERE username='"+ username_alphaf_lowercase +"'"
    cur.execute(query)
    check = cur.fetchone()

    if check == None:
        token_check = "SELECT * FROM alphaf_users WHERE token='"+ token_alphaf +"'"
        cur.execute(token_check)
        check_token = cur.fetchone()
        if check_token == None:
            print()
            print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Invalid token. Please try again")
            time.sleep(2)
            startup_menu()
        else:   
            if "YES" in check_token:
                print()
                print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Token already in use")
                time.sleep(2)
                cur.close()
                connection.close()
                startup_menu()
            else:
                newuser = "UPDATE alphaf_users SET email='"+ email_alphaf +"', username='"+ username_alphaf_lowercase +"',password='"+ password_alphaf +"',active='YES', reg_ip='"+ public_ip +"' WHERE alphaf_users.token ='"+ token_alphaf +"'"
                cur.execute(newuser)
                connection.commit()
                print()
                print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Account successfully created")
                time.sleep(2)
                cur.close()
                connection.close()
                startup_menu()
    else:
        print()
        print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Username already taken")
        time.sleep(2)
        startup_menu()
#----------END----------

#Login Menu
def login():
    print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Connecting to server")
    ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Sign In")
    logo()
    mysql_check()
    username_alphaf = input(WHITE + "[" + MAGENTA + "Username" + WHITE + "] >>> ")
    password_alphaf = input(WHITE + "[" + MAGENTA + "Password" + WHITE + "] >>> ")
    cur = connection.cursor()
    username_alphaf_lowercase = username_alphaf.lower()
    query = "SELECT username,password,banned FROM alphaf_users WHERE username='"+ username_alphaf_lowercase +"' AND password='" + password_alphaf + "'"
    cur.execute(query)
    user_check = cur.fetchone()
    if user_check == None:
        print()
        print(WHITE + "[" + CYAN + "MAGENTA-F" + WHITE + "] >>> Inncorrect username or password")
        time.sleep(2)
        startup_menu()
    else:
        if username_alphaf_lowercase in user_check and password_alphaf in user_check:
            if "YES" in user_check:
                print()
                print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Account has been banned by an Admin")
                time.sleep(3)
                startup_menu()
            else:
                print()
                print(WHITE + "[" + MAGENTA + "Signing in as " + YELLOW + username_alphaf + WHITE + "]")
                global loginid
                loginid = username_alphaf_lowercase
                if loginid=="admin":
                    time.sleep(2)
                    main_admin()
                    update_last_login_ip = "UPDATE alphaf_users SET last_ip='"+ public_ip +"' WHERE alphaf_users.username ='"+ username_alphaf +"'"
                    cur.execute(update_last_login_ip)
                    connection.commit()
                    cur.close()
                    connection.close()
                else:
                    time.sleep(2)
                    update_last_login_ip = "UPDATE alphaf_users SET last_ip='"+ public_ip +"' WHERE alphaf_users.username ='"+ username_alphaf +"'"
                    cur.execute(update_last_login_ip)
                    connection.commit()
                    main()
                    cur.close()
                    connection.close()
        else:
            print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> There was an error.")
            time.sleep(2)
            startup_menu()
#----------END----------

#Admin Menu
def main_admin():
    print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Checking")
    ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Main Menu For Admins")
    logo()
    print(WHITE + "[" + MAGENTA + "Welcome Back, " + YELLOW + loginid + WHITE + "]")
    print()
    print(WHITE + "[" + MAGENTA + "1" + WHITE + "] Check User")
    print(WHITE + "[" + MAGENTA + "2" + WHITE + "] Change User Password")
    print(WHITE + "[" + MAGENTA + "3" + WHITE + "] Ban User")
    print(WHITE + "[" + MAGENTA + "4" + WHITE + "] Generate Token")
    print(WHITE + "[" + MAGENTA + "0" + WHITE + "] Logout")
    print()
    admin_option = input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> ")

    if admin_option == "1":
        ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Check User Menu")
        logo()
        check_user = input(WHITE + "[" + MAGENTA + "Alpha-F Username" + WHITE + "] >>> ")
        mysql_check()
        cur = connection.cursor()
        idd = "SELECT id FROM alphaf_users WHERE username='"+ check_user +"'"
        username = "SELECT username FROM alphaf_users WHERE username='"+ check_user +"'"
        email = "SELECT email FROM alphaf_users WHERE username='"+ check_user +"'"
        token = "SELECT token FROM alphaf_users WHERE username='"+ check_user +"'"
        banned = "SELECT banned FROM alphaf_users WHERE username='"+ check_user +"'"
        reg_ip = "SELECT reg_ip FROM alphaf_users WHERE username='"+ check_user +"'"
        last_ip = "SELECT last_ip FROM alphaf_users WHERE username='"+ check_user +"'"
        cur.execute(username)
        find_username = cur.fetchone()
        if find_username == None:
            print()
            print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Could not find user in database")
            time.sleep(2)
            main_admin()
        else:
            cur.execute(idd)
            find_id = cur.fetchone()
            cur.execute(email)
            find_email = cur.fetchone()
            cur.execute(token)
            find_token = cur.fetchone()
            cur.execute(banned)
            find_banned = cur.fetchone()
            cur.execute(last_ip)
            find_last_ip = cur.fetchone()
            cur.execute(reg_ip)
            find_reg_ip = cur.fetchone()

            find_reg_ip_str = str(find_reg_ip)
            find_last_ip_str = str(find_last_ip)
            find_token_str = str(find_token)
            find_email_str = str(find_email)
            find_banned_str = str(find_banned)
            find_id_str = str(find_id)
            find_username_str = str(find_username)

            bad_chars = ['(', ')', ',', "'"]
            for i in bad_chars :
                find_token_str = find_token_str.replace(i, '')
                find_email_str = find_email_str.replace(i, '')
                find_banned_str = find_banned_str.replace(i, '')
                find_last_ip_str = find_last_ip_str.replace(i, '')
                find_id_str = find_id_str.replace(i, '')
                find_username_str = find_username_str.replace(i, '')
                find_reg_ip_str = find_reg_ip_str.replace(i, '')
            print()
            print(WHITE + "[" + MAGENTA + "ID" + WHITE + "] >>> " + str(find_id_str))
            print(WHITE + "[" + MAGENTA + "Email" + WHITE + "] >>> " + str(find_email_str))
            print(WHITE + "[" + MAGENTA + "Username" + WHITE + "] >>> " + str(find_username_str))
            print(WHITE + "[" + MAGENTA + "Token" + WHITE + "] >>> " + str(find_token_str))
            print(WHITE + "[" + MAGENTA + "Banned" + WHITE + "] >>> " + str(find_banned_str))
            print(WHITE + "[" + MAGENTA + "Register IP" + WHITE + "] >>> " + str(find_reg_ip_str))
            print(WHITE + "[" + MAGENTA + "Last Login IP" + WHITE + "] >>> " + str(find_last_ip_str))
            print()
            input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Press any key to continue")
            cur.close()
            connection.close()
            main_admin()

    elif admin_option == "2":
        ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Change Password Menu")
        logo()
        mysql_check()
        change_user_password = input(WHITE + "[" + MAGENTA + "Username" + WHITE + "] >>> ")
        if change_user_password == "Admin":
            print()
            print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> You are not allowed to change admin password.")
            print()
            ir = input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Press any key to continue")
            main_admin()
        else:
            cur = connection.cursor()
            user = "SELECT username,password FROM alphaf_users WHERE username='"+ change_user_password +"'"
            cur.execute(user)
            find_username = cur.fetchone()
            if find_username == None:
                print()
                print(WHITE + "[" + MAGENTA + "AlphaF" + WHITE + "] >>> Could not find user in database")
                time.sleep(3)
                main_admin()
            else:
                print()
                new_password = input(WHITE + "[" + MAGENTA + "New password" + WHITE + "] >>> ")
                updated_password = "UPDATE alphaf_users SET password='"+ new_password +"' WHERE alphaf_users.username ='"+ change_user_password +"'"
                cur.execute(updated_password)
                connection.commit()
                time.sleep(1)
                print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Password for '"+ YELLOW + change_user_password + WHITE +"' has been updated")
                print()
                ir = input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Press any key to continue")
                cur.close()
                connection.close()
                main_admin()

    elif admin_option == "3":
        ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Ban User Menu")
        logo()
        mysql_check()
        print(WHITE + "[" + MAGENTA + "1" + WHITE + "] Ban User")
        print(WHITE + "[" + MAGENTA + "2" + WHITE + "] Unban User")
        print(WHITE + "[" + MAGENTA + "0" + WHITE + "] Go Back")
        print()
        admin_ban = input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> ")

        if admin_ban == "1":
            logo()
            print()
            admin_option = input(WHITE + "[" + MAGENTA + "Username" + WHITE + "] >>> ")
            if admin_option == "Admin":
                print()
                print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Cannot ban " + YELLOW + "Admin" + WHITE + " account")
                time.sleep(2)
                main_admin()
            else:
                cur = connection.cursor()
                user = "SELECT username FROM alphaf_users WHERE username='"+ admin_option +"'"
                cur.execute(user)
                find_user = cur.fetchone()
                if find_user == None:
                    print()
                    print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Could not find user in database")
                    time.sleep(2)
                    main_admin()
                else:
                    update_ban = "UPDATE alphaf_users SET banned='YES' WHERE alphaf_users.username ='"+ admin_option +"'"
                    cur.execute(update_ban)
                    connection.commit()
                    print()
                    print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> " + YELLOW + admin_option + WHITE +" has been banned")
                    time.sleep(2)
                    cur.close()
                    connection.close()
                    main_admin()

        elif admin_ban == "2":
            logo()
            print()
            admin_option = input(WHITE + "[" + MAGENTA + "Username" + WHITE + "] >>> ")
            cur = connection.cursor()
            user = "SELECT username FROM alphaf_users WHERE username='"+ admin_option +"'"
            cur.execute(user)
            find_user = cur.fetchone()
            if find_user == None:
                print()
                print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Could not find user in database")
                time.sleep(2)
                main_admin()
            else:
                update_ban = "UPDATE alphaf_users SET banned='' WHERE alphaf_users.username ='"+ admin_option +"'"
                cur.execute(update_ban)
                connection.commit()
                print()
                print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> "+ YELLOW + admin_option + WHITE +" has been unbanned")
                time.sleep(2)
                cur.close()
                connection.close()
                main_admin()

        elif admin_ban == "0":
            main_admin()
            pass

        else:
            print()
            print(WHITE + "[" + MAGENTA + "AlphaF" + WHITE + "] >>> Invalid Command")
            time.sleep(2)
            main_admin()

    elif admin_option == "4":
        ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Generate Token Menu")
        logo()
        mysql_check()
        amount_tokens = input(WHITE + "[" + MAGENTA + "Amount of tokens" + WHITE + "] >>> ")
        print()
        uppercase_letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
        lowercase_letters = uppercase_letters.lower()
        digits = "0123456789"

        upper, lower, nums = True, True, True

        all = ""

        if upper:
            all += uppercase_letters
        if lower:
            all += lowercase_letters
        if nums:
            all += digits

        length = 15
        amount = int(amount_tokens)

        for x in range(amount):
            cur = connection.cursor()
            gen_tokens = "".join(random.sample(all, length))
            print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> " + gen_tokens)
            new_tokens = "INSERT INTO alphaf_users (`id`, `token`) VALUES (NULL, '" + gen_tokens + "');"
            cur.execute(new_tokens)
            connection.commit()
            time.sleep(0.5)
        print()
        ir = input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Press any key to continue")
        cur.close()
        connection.close()
        main_admin()

    elif admin_option == "0":
        print()
        print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Signing out")
        time.sleep(2)
        startup_menu()

    else:
        print()
        print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Invalid command")
        time.sleep(2)
        main_admin()
#----------END----------

#Main Menu
def main():
    ctypes.windll.kernel32.SetConsoleTitleW("Alpha-F | Main Menu")
    logo()
    print(WHITE + "[" + MAGENTA + "Welcome back, " + YELLOW + loginid + WHITE + "]")
    print()
    print(WHITE + "[" + MAGENTA + "1" + WHITE + "] Malicious Menu")
    print(WHITE + "[" + MAGENTA + "2" + WHITE + "] Proxy Menu")
    print(WHITE + "[" + MAGENTA + "3" + WHITE + "] Checker Menu")
    print(WHITE + "[" + MAGENTA + "0" + WHITE + "] Logout")
    print()
    main_option = input(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> ")

    if main_option == "1":
        development()
        main()
        pass

    elif main_option == "2":
        development()
        main()
        pass

    elif main_option == "3":
        development()
        main()
        pass

    elif main_option == "0":
        print()
        print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Signing out")
        time.sleep(2)
        startup_menu()
    else:
        print()
        print(WHITE + "[" + MAGENTA + "Alpha-F" + WHITE + "] >>> Invalid command")
        time.sleep(2)
        main()
#----------END----------

startup_menu()
