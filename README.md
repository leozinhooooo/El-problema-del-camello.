def solve_expression(expr):
    smax = []
    smin = []
    tmp = 0
    op = '+'
    
    for i in range(len(expr) + 1):
        if i < len(expr) and expr[i].isdigit():
            tmp = tmp * 10 + int(expr[i])
        else:
            if op == '+':
                if smax:
                    smax[-1] += tmp
                else:
                    smax.append(tmp)
                smin.append(tmp)
            else:
                if smin:
                    smin[-1] *= tmp
                else:
                    smin.append(tmp)
                smax.append(tmp)
            if i < len(expr):
                op = expr[i]
            tmp = 0
    
    amax = 1
    for num in smax:
        amax *= num
    
    amin = sum(smin)
    
    return amax, amin

n = int(input())
for _ in range(n):
    expr = input()
    maximum, minimum = solve_expression(expr)
    print(f"The maximum and minimum are {maximum} and {minimum}.")

