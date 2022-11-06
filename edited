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
    '''
    메뉴를 프린트 하는 함수\n
    =========순발력 테스트 게임===========\n
    [1] 시작하기\n
    [-1] 나가기\n
    처럼 나와야 한다. 다른 동작은 하지 않는다.
    '''
    print("=========순발력 테스트 게임===========\n [1] 시작하기\n[-1] 나가기\n입력하세요 : ", end='')
def get_command()->int:
    '''
    입력을 받는 함수
    입력을 받아 정수형으로 변경해 리턴해준다.
    만약 정수형이 아닐 경우에는 -1을 리턴한다.
    만약 입력받은 정수가 1 혹은 -1이 아닐 경우 -1을 리턴한다.
    '''
    a = input()
    if a == "1":
        return 1
    return -1
def get_name()-> str:
    '''
    유저 이름을 입력받는다.
    유저 이름이 3글자가 아닐 경우
    다시 입력받는다.
    이름을 리턴한다.
    '''
    print("이름을 입력하십시오")
    what_is_your_name = input()
    while len(what_is_your_name) != 3:
        print("이름을 세 글자로 다시 입력해 주시길 바랍니다")
        what_is_your_name = input()
    return what_is_your_name

def get_difficulty() -> int:
    '''
    난이도를 입력 받는다.
    정수나 잘못된 난이도(1,2,3)이 아닌
    값을 입력 받는다면 다시 입력받는다.
    '''
    difficulty = input("난이도를 설정하라\n 난이도엔 1 2 3 이 있음 : ")
    while difficulty not in ["1", "2", "3"]:
        print("난이도를 다시 설정하셈")
        difficulty = input()
    return int(difficulty)
def show_round_info(current_round:int)->None:
    '''
		현재 라운드가 몇번째 라운드인지 보여준다.
		'''
    print(current_round)


def show_difficulty_info(difficulty : int) -> None:
    '''
    난이도에 따라 난이도에 맞는 키들을 보여준다.
    '''
    print(difficulty_to_keys_map[difficulty])
    
def choose_random_key(difficulty: int) -> str:    
    '''
    난이도에 따라 난이도에 맞는 키 중 하나를 랜덤으로 반환한다.
    '''
    return random.choice(difficulty_to_keys_map[difficulty])
def get_random_time()-> float:
    '''
    랜덤한 시간(1~5초) 사이에 시간을 리턴한다.
    '''
    return (random.random() * 4) + 1

def show_target_key(key: str) -> None:
    '''
    대상 키를 10번 반복해서 보여준다.
    '''
    print(f"PRESS {key  * 5}")

def wait_for_key(key: str) -> float:
    '''
    대상 키가 눌러졌다면 눌러지기까지의 초를 리턴한다.
    잘못된 키가 눌러진다면 -1을 리턴한다.
    힌트 https://stackoverflow.com/questions/70793120/is-there-a-function-in-the-keyboard-module-that-returns-any-letter-that-is-press
    '''
    start_time = time.time()
    tmp = keyboard.read_key()
    if tmp == key:
        return time.time() - start_time
    else:
        return -1


    
def round(difficulty : int, current_round : int) -> float:
    '''
    난이도 현재 라운드를 받아 라운드를 수행한다.\n
    show_round_info 함수를 호출해 현재 라운드 정보를 보여준다\n
    show_difficulty_info 함수를 호출해 난이도 정보와 후보 키를 보여준다.\n
    choose_random_key 함수를 랜덤한 키를 받는다. \n
    get_random_time 함수를 호출에 결과만큼 sleep 후\n
    show_target_key 함수를 호출에 입력해야하는 키를 보여준다.\n
    유저가 해당 키를 입력하는 시간을 기록해 리턴한다.\n
    만약 랜덤한 시간이 지나기 전에 어느 키든 입력하거나, \n
    시간이 다되고 잘못된 키를 입력하는 경우\n
    -1을 리턴한다.
    '''
    show_round_info(current_round)
    show_difficulty_info(difficulty)
    key = choose_random_key(difficulty)
    t=  get_random_time()
    time.sleep(t)
    show_target_key(key)
    return wait_for_key(key)
    
    
    
def game() -> None:
    '''
    게임을 수행하는 함수 
    닉네임을 입력 받는 함수를 실행하고
    게임 난이도를 입력 받는 함수를 실행해
    게임을 시작한다.
    게임은 5 라운드로 이루어져있다.
    라운드의 결과가 -1일 경우 해당 라운드를 다시 시작한다.
    '''

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
    '''
    입력 받은 command에 따라 다른 기능을 수행한다.
    '''
    if command == 1:
        game()
    elif command == -1:
        # 종료
        pass

def main() -> None:
    '''
    메뉴를 보여주고
    입력을 받는다.
    실행
    '''
    show_menu()
    command : int = get_command()
    run(command)

while True:
    main()
