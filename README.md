from random import randrange

hp = 100
sanity = 100
hp_medicine = 3
sanity_medicine = 3
pochoden = 3


def fight():
    global random_final, random_damage, enemy_hp, hp
    print("Zaútočili na vás!")
    enemy_hp = 100
    while True:
        if enemy_hp <= 0:
            print("Vyhrál jste!")
        elif hp <= 0:
            print("Prohrál jste!")
        
        random_value = randrange(0, 100)
        random_value_enemy = randrange (0, 100)
        random_calculate = random_value % 2
        random_calculate_enemy = random_value_enemy %2
        if random_calculate == 1:
            random_final = True
        else:
            random_final = False
        if random_calculate_enemy == 1:
            random_final_enemy = True
        else:
            random_final_enemy = False
        random_damage = randrange(15, 30)
        random_damage_enemy = randrange(10, 20)
        try:        
            print("1. Útok")
            print("2. Krytí")
            respond = int(input("Zvolte možnost. (1/2):   "))
            
            if respond == 1:
                print("Pokusil jste se zaútočit na nepřítele!")
                if random_final == True:
                    print("Trefil jste se!")
                    enemy_hp = enemy_hp - random_damage
                    if random_damage >= 25 and random_damage <= 30:
                        print(f"Udělil jste kritický zásah za {random_damage}HP!")
                        if enemy_hp > 0:
                            print(f"Nepřítel má nyní {enemy_hp}HP")
                        elif enemy_hp <= 0:
                            print("Zneškodnil jste nepřítele!")
                            eval(return_function + "()")
                    else:
                        print(f"Udělil jste poškození za {random_damage}HP!")
                        if enemy_hp > 0:
                            print(f"Nepřítel má nyní {enemy_hp}HP")
                        elif enemy_hp <= 0:
                            print("Zneškodnil jste nepřítele!")
                            eval(return_function + "()")
                    if random_final_enemy == True:
                        print(f"Nepřítel vám udělil poškození za {random_damage_enemy}HP!")
                        hp = hp - random_damage_enemy
                        check_stats()
                    else:
                        print("Nepřítel minul. Jste na tahu!")
                elif random_final == False:
                    print("Minul jste se!")
                    if random_final_enemy == True:
                        print(f"Nepřítel vám udělil poškození za {random_damage_enemy}HP!")
                        hp = hp - random_damage_enemy
                        check_stats()
                    else:
                        print("Nepřítel minul. Jste na tahu!")
            elif respond == 2:
                print("Schoval jste se za nejbližší kryt.")
                if random_final == True:
                    print("Nepřítel vás netrefil!")
                elif random_final == False:
                    if random_final_enemy == True:
                        print(f"Nepřítel vám udělil poškození za {random_damage_enemy}HP!")
                        hp = hp - random_damage_enemy
                        check_stats()
                    else:
                        print("Nepřítel minul. Jste na tahu!")
                
        except ValueError:
            print("Napište 1, nebo 2!")



def check_stats():
    global hp, sanity
    print(f"Rozum = {sanity}%")
    print(f"Zdraví = {hp}%")
    if hp <= 0:
        print("Umřel jste!")
        exit()
    
    if sanity > 25:
        print("Váš rozum je v pořádku.")
    elif sanity <= 25 and sanity >= 1:
        print("Začínáte pomalu šílet, měl by jste si vzít medicínu!")
    elif sanity <= 0:
        print("Zbláznil jste se! Nemůžete pokračovat v cestě za dobrodružstvím!")
        exit()

def medicine(return_function):
    global hp, sanity, hp_medicine, sanity_medicine
    print(f"1. Vzít si léky na rozum (Zbývá: {sanity_medicine})")
    print(f"2. Vzít si léky na zdraví (Zbývá: {hp_medicine})")
    print("3. Pokračovat ve hře")
    print("""
    
            """)
    while True:
        try:
            medicine_choice = int(input("Na co si chcete vzít léky? (1/2/3)"))
            if medicine_choice == 1:
                sanity_medicine = sanity_medicine - 1
                if sanity_medicine == 0:
                    print("Nemáte dostatek léků!")
                else:
                    print("Vypil jste léky! +20 procent rozumu")
                    sanity = sanity + 20
                    check_stats()
            elif medicine_choice == 2:
                hp_medicine = hp_medicine - 1
                if hp_medicine == 0:
                    print("Nemáte dostatek léků!")
                else:
                    print("Vypil jste léky! +20 procent zdraví")
                    hp = hp + 20
                    check_stats()
            elif medicine_choice == 3:
                break
            else:
                print("Napište 1, 2 nebo 3!")
        except ValueError:
            print("Napište 1, 2 nebo 3!")
    eval(return_function + "()")

def start_game():
    print("Vítejte v Stínech záhrobí!")
    print("""V daleké zemi Vymíra, kde se hranice mezi životem a smrtí tenčí,
    leží tajemné město Záhrobí. Toto místo bylo kdysi prosperujícím centrem magie a umění, 
    ale nyní je zahaleno v temnotě a strachu. Záhrobí obývají duchové, nemrtví a různé přízraky, 
    které se potulují ulicemi a skrývají se v ruinách starobylých budov.
        
    Vaše družina dobrodruhů byla najata tajemným mecenášem, 
    aby vyšetřila náhlé zvýšení aktivity nemrtvých v Záhrobí. 
    Něco probudilo síly, které by měly zůstat spící, a vy máte zjistit co, 
    a pokud možno to zastavit.""")
    choice1()

def choice1():
    check_stats()
    print("Momentálně se nacházíte před hřbitovem")
    print("1. Prozkoumat hřbitov")
    print("2. Pokračovat dál do temného lesa")
    print("3. Vzít léky.")
    print("""
    
            """)
    
    while True:
        try:
            respond = int(input("Zvolte odpověď. (1/2/3)"))
            
            if respond == 1:
                hrbitov()
                break
            elif respond == 2:
                temny_les()
                break
            elif respond == 3:
                medicine("choice1")
            else:
                print("Napiště 1, 2, nebo 3")
        except ValueError:
            print("Napiště 1, 2, nebo 3")

def hrbitov():
    global hp, sanity
    print("""Vešli jste do hřbitova hlavní bránou, procházíte se hřibovem a hledáte něco zajímavého.
    když už jste u starobylého kostelíka, tak se rozrazily dveře a vyběhla na vás banda revenantů!
        
    Bohužel jich bylo příliš moc a nedokázali jste je překonat. 
    Naštěstí jeden z členů družiny zapálil pochodeň, pomocí které revenanty aspoň na chvíli odehnal!
    -25 procent zdraví
    -20 procent rozumu""")
    hp = hp - 25
    sanity = sanity - 20
    check_stats()
    print("")
    print("")
    print("""Po zotavení jste se rozhodli dokončit průzkum hřibova a dorazili jste k druhému vchodu. 
Po pravé straně se nachází temný les, po levé straně vidíte pouze cestičku.""")
    print("""1. Jít do temného lesa
2. Jít po cestičce
3. Vzít si léky""")
    while True:
        try:
            respond = int(input("Zvolte odpověď. (1/2/3)"))
            
            if respond == 1:
                temny_les()
                break
            elif respond == 2:
                cesticka()
                break
            elif respond == 3:
                medicine("hrbitov")
            else:
                print("Napiště 1, 2, nebo 3")
        except ValueError:
            print("Napiště 1, 2, nebo 3")

def temny_les():
    global hp, sanity
    
    

def cesticka():
    global hp, sanity, pochoden
    print("""Cesta je velmi temná a nejde téměř nic vidět.""")
    
    while True:
        try:
            respond = int(input(f"""Chcete zapálit na cestu pochodeň? Pochodní zbývá: {pochoden}.
                        1. Ano
                        2. Ne
                        3. Léky"""))
            if respond == 1:
                print("Zapálil jste pochoděň!")
                pochoden = pochoden - 1
                print(f"Pochodní zbývá: {pochoden}")
                respond_pochoden = True
                break
            elif respond == 2:
                print("Celou cestu půjdete po tmě.")
                print(f"Pochodní zbývá: {pochoden}")
                respond_pochoden = False
                break
            elif respond == 3:
                medicine("cesticka")
            else:
                print("Napiště 1, 2, nebo 3")
        except ValueError:
            print("Napiště 1, 2, nebo 3")

    if respond_pochoden == True:
        print("""Díky pochodni jste ušetřili velké procenta rozumu a možná jste se i vyhli útoku revenantů!""")
    else:
        print("""Šli jste dlouhou trasu po téměř kompletní tmě. 
            Slyšeli jste blízko sebe hlasité pazvuky a skřeky.
            Vaše procenta rozumu klesla o 25%!""")
        sanity = sanity - 25
    check_stats()
    print("Došli jste k velkému opuštěnému domu.")

    while True:
        try:
            check_stats()
            print("1. Prozkoumat budovu")
            respond = int(input("2. Pokračovat po cestičce  (1/2): "))
            if respond == 1:
                pruzkum_budovy()
                break
            elif respond == 2:
                pokracovani_cesty()
                break
            else:
                print("Napište 1, nebo 2!")
        except ValueError:
            print("Napište 1, nebo 2!")

def pruzkum_budovy():
    global hp, sanity, pochoden
    print("Po otevření dveří do staré budovy jste zjistili, že je budova příliš temná a opět nejde nic vidět.")
    check_stats()
    while True:
        try:
            respond = int(input(f"""Chcete zapálit pochodeň před vstupem do baráku? Pochodní zbývá: {pochoden}.
                        1. Ano
                        2. Ne
                        3. Léky"""))
            if respond == 1:
                print("Zapálil jste pochoděň!")
                pochoden = pochoden - 1
                print(f"Pochodní zbývá: {pochoden}")
                respond_pochoden = True
                break
            elif respond == 2:
                print("Vydáváte se do budovy bez světla!")
                print(f"Pochodní zbývá: {pochoden}")
                respond_pochoden = False
                break
            elif respond == 3:
                medicine("pruzkum_budovy")
            else:
                print("Napiště 1, 2, nebo 3")
        except ValueError:
            print("Napiště 1, 2, nebo 3")
        

def pokracovani_cesty():
    global hp, sanity
        






if __name__ == "__main__":
    fight()
