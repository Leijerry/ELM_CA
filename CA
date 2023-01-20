urban_proba = np.loadtxt('C:\\Users\\Administrator\\Desktop\\概率.txt')
urban_start = np.loadtxt('D:\\CA\\2018.txt')
landuse_start = np.loadtxt('C:\\Users\\Administrator\\Desktop\\2018-1.txt')
def ca():
    num = 0
    while num < 1:
        index = np.argwhere((urban_proba != -9999) & (urban_start != 1)) # 将非城市的栅格找出来(把等于1和无效的区域排除)
        for i, (row, col) in enumerate(index[:]):
            s = landuse_start[row-1:row+2, col-1:col+2]
            if urban_start[row, col] != 1:
                tp = (len(s[s == 1]) / (8 - len(s[s == -9999]))) * urban_proba[row, col] * (0 if landuse_start[row, col] == 3 or landuse_start[row, col] == 4 else 1)
                urban_proba[row, col] = tp
                # print(i)
        a = urban_proba.flatten() # 将预测的概率值打平
        a[a == 1] = -1 # 将等于1的赋值为-1
        if num != 1: # 迭代次数+1
            n = heapq.nlargest(281, range(len(a)), a.take) # 选择总的前281个，总共迭代两次,总共增加的城市栅格的数目
            print(len(n))
        else:
            n = heapq.nlargest(8, range(len(a)), a.take) # 最后余数
        for i in n:
            urban_proba[i//691, i % 691] = 1  # 将打平之后的索引还原成为原来的的索引
            landuse_start[i//691, i % 691] = 1
            urban_start[i//691, i % 691] = 1
        num += 1
        print(len(urban_start[urban_start == 1]))
        print(num)
    return [urban_proba, landuse_start, urban_start]


x1,x2,x3=ca()
np.savetxt("test2.txt", x3)
