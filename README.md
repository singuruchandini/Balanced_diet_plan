u# Balanced_diet_plan
The Balanced Diet Plan project is a Python-based application designed to help users create and maintain a healthy, balanced diet plan tailored to their needs. This project combines the principles of nutrition science with programming to generate customized meal plans, track caloric intake, and promote healthier eating habits.
def main():
    a = input().strip()
    res = 0
    p = c = f = 0
    a_len = len(a)

    for i in range(a_len):
        if a[i] == ' ':
            continue
        if a[i].isdigit():
            res = res * 10 + int(a[i])
        else:
            if a[i] == 'P':
                p = res
            elif a[i] == 'C':
                c = res
            else:
                f = res
            res = 0

    b = input().strip()
    pp = cc = ff = 0
    ans = []
    res = 0
    mi = float('inf')
    sump = sumc = sumf = 0
    b_len = len(b)

    for i in range(b_len):
        if b[i] == ' ':
            continue
        if b[i] == '|':
            ans.append((pp, (cc, ff)))
            pp = cc = ff = 0
        elif b[i].isdigit():
            res = res * 10 + int(b[i])
        else:
            if b[i] == 'P':
                pp = res
                sump += pp
            elif b[i] == 'C':
                cc = res
                sumc += cc
            else:
                ff = res
                sumf += ff
            res = 0

    ans.append((pp, (cc, ff)))

    if sump:
        mi = min(mi, p // sump)
    if sumc:
        mi = min(mi, c // sumc)
    if sumf:
        mi = min(mi, f // sumf)
    if mi == float('inf'):
        mi = 0

    nn = len(ans)
    lef = (p - mi * sump, (c - mi * sumc, f - mi * sumf))
    ma = (0, (0, 0))
    
    # Iterate through all subsets
    for i in range(1 << nn):
        curr = (0, (0, 0))
        for j in range(nn):
            if i & (1 << j):
                curr = (curr[0] + ans[j][0], 
                        (curr[1][0] + ans[j][1][0], curr[1][1] + ans[j][1][1]))

        if (curr[0] <= lef[0] and curr[1][0] <= lef[1][0] and curr[1][1] <= lef[1][1]):
            ma = max(ma, curr)

    print(p - sump * mi - ma[0], c - sumc * mi - ma[1][0], f - sumf * mi - ma[1][1])

if __name__ == "__main__":
    main()
