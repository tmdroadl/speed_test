"# speed_test"
import random
import time

import keyboard

difficulty_to_keys_map = {
    1: ['space'],
    2: ['space', 'enter', 'up'],
    3: ['space', 'enter', 'up', 'left', 'down', 'right']
}

def show_menu()->None:
    print("=========순발력 테스트 게임===========\n [1] 시작하기\n[-1] 나가기\n입력하세요 : ", end='')
def get_command()->int:
    a = input()
    if a == "1":
        return 1
    return -1
def get_name()-> str:

    print("이름을 입력하십시오")
    what_is_your_name = input()
    while len(what_is_your_name) != 3:
        print("이름을 세 글자로 다시 입력해 주시길 바랍니다")
        what_is_your_name = input()
    return what_is_your_name

def get_difficulty() -> int:

    difficulty = input("난이도를 설정하라\n 난이도엔 1 2 3 이 있음 : ")
    while difficulty not in ["1", "2", "3"]:
        print("난이도를 다시 설정하셈")
        difficulty = input()
    return int(difficulty)
def show_round_info(current_round:int)->None:

    print(current_round)


def show_difficulty_info(difficulty : int) -> None:

    print(difficulty_to_keys_map[difficulty])
    
def choose_random_key(difficulty: int) -> str:    

    return random.choice(difficulty_to_keys_map[difficulty])
def get_random_time()-> float:

    return (random.random() * 4) + 1

def show_target_key(key: str) -> None:

    print(f"PRESS {key  * 5}")

def wait_for_key(key: str) -> float:

    start_time = time.time()
    tmp = keyboard.read_key()
    if tmp == key:
        return time.time() - start_time
    else:
        return -1


    
def round(difficulty : int, current_round : int) -> float:

    show_round_info(current_round)
    show_difficulty_info(difficulty)
    key = choose_random_key(difficulty)
    t=  get_random_time()
    time.sleep(t)
    show_target_key(key)
    return wait_for_key(key)
    
    
    
def game() -> None:


    score = 0
    name = get_name()
    difficulty= get_difficulty()
    i = 1
    while i < 6:  
        result = round(difficulty, i)
        if result== -1:
            continue
        score += result
        i += 1

    print(f'{name}님의 성적은 {int(score * 1000// 5)}ms')


def run(command : int) -> None:
    if command == 1:
        game()
    elif command == -1:
        # 종료
        pass

def main() -> None:
    show_menu()
    command : int = get_command()
    run(command)

while True:
    main()
