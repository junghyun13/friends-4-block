# friends-4-block
# m is vertical and n is horizontal, and there are blocks called R,M,A,F,N,T,J,C. If there are 4 identical blocks, they disappear (possibly overlapping), and when they disappear, the blocks above come down. Find the total number of disappearing blocks! m은 세로이고 n은 가로이고 R,M,A,F,N,T,J,C라는 블록들이 있다. 4개씩 같은 블록이 있으면 사라지고 (겹쳐있는 것도 가능) 사라지면 위에 있던 블럭들은 내려오게 되는데  사라지는 블록이 총 몇개인지를 구해라!
# python
# case 1:
def solution(m, n, board):
    for i in range(m):
        board[i] = list(board[i])
    cnt = 0
    rm = set()
    while True: # 보드를 순회하며 4블록이 된 곳의 좌표를 집합에 기록
        for i in range(m-1):
            for j in range(n-1):
                t = board[i][j]
                if t == []:
                    continue
                if board[i+1][j] == t and board[i][j+1] == t and board[i+1][j+1] == t:
                    rm.add((i,j))
                    rm.add((i+1,j))
                    rm.add((i,j+1))
                    rm.add((i+1,j+1))
        if rm: # 좌표가 존재한다면 집합의 길이만큼 세주고 블록을 지움 
            cnt += len(rm)
            for i,j in rm:
                board[i][j] = []
            rm = set()
        else: # 없다면 함수 종료
            return cnt
        while True: # 블록을 위에서 아래로 당겨줌
            moved = 0
            for i in range(m-1):
                for j in range(n):
                    if board[i][j] and board[i+1][j]==[]:
                        board[i+1][j] = board[i][j]
                        board[i][j] = []
                        moved = 1
            if moved == 0:
                break
board=["CCBDE", "AAADE", "AAABF", "CCBBF"]
a=solution(4,5,board)
print(a)
# case 2:
def solution(m, n, board):
    x = board
    x2 =[]
    for i in x: 
        x1 = []
        for i2 in i:
            x1.append(i2)
        x2.append(x1)
    point = 1
    while point != 0:
        list = []
        point = 0
        for i in range(m - 1):
            for j in range(n - 1):
                if x2[i][j] == x2[i][j + 1] == x2[i + 1][j] == x2[i + 1][j + 1] != '팡!':
                    list.append([i, j])
                    point += 1
        for i2 in list:
            i, j = i2[0], i2[1]
            x2[i][j], x2[i][j + 1], x2[i + 1][j], x2[i + 1][j + 1] = '팡!', '팡!', '팡!', '팡!'
        for i3 in range(m):
            for i in range(m - 1):
                for j in range(n):
                    if x2[i + 1][j] == '팡!':
                        x2[i + 1][j], x2[i][j] = x2[i][j], '팡!'
    cnt = 0
    for i in x2:
        cnt += i.count('팡!')
    return cnt
#result--> 14
