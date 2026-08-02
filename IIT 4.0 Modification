import numpy as np
import math 
import itertools
import random 
from numpy.random import default_rng
set_number=int(input('set nummber= '))
i_first=1
U=list(itertools.product([0,1], repeat=set_number))
print('U= ', U)
u= np.random.randint(0, 2, size=set_number)
print('u= ', u)
for i in range(set_number):
    Ui={i}
    ui=u[i]
S=set(random.sample(range(set_number), random.randint(1, set_number-1)))
print('S= ', S)
W=set(range(set_number))-S
print('W= ', W) # разность множеств индексов
s_size = random.randint(1, set_number - 1)  # размер подсистемы: 1 или 2
s = np.array([u[i] for i in sorted(S)])  # вектор
print('s= ', s)
w = np.array([u[i] for i in sorted(W)])
print('w= ', w)
for i in S:
    Si={i}
    si= s[list(sorted(S)).index(i)]
print('Si= ', Si)
print('si= ', si)
m_size = random.randint(2, len(S)) if len(S) >= 2 else 1
M = set(random.sample(list(S), m_size))
print('M= ', M)
m = np.array([u[i] for i in sorted(M)])# Состояния механизма m
print('m= ', m)
for i in M:
    Mi = {i}      # Локальное множество узла механизма
    mi = m[list(sorted(M)).index(i)]  if len(m)>1 else m
    print('mi= ', mi)# Локальное состояние узла механизма
z_size = random.randint(2, len(S)) if len(S) >= 2 else 1
Z = set(random.sample(list(S), z_size))
print('Z= ', Z)
z = np.array([u[i] for i in sorted(Z)])
print('z= ', z)
for i in Z:
    Zi = {i}      # Локальное множество узла пурвита
    zi = z[list(sorted(Z)).index(i)]  if len(z)>1 else z
    print('z[i]= ', zi)# Локальное состояние узла пурвита
z_hat=np.array(z).flatten()
print('z_hat= ', z_hat) 
S_hat=S
print('S_hat= ', S)
s_hat=np.array([u[i] for i in sorted(S)])
print('s_hat= ', s_hat)
g=np.sum(s_hat)
j=g
print('j= ', j)
n=s.shape[0]
b=random.randint(0,2)
print('b= ', b)
bj=b*j
print('bj= ', bj)
b_list = {j: random.randint(0, 2) for j in S}
print('b_list= ', b_list)
for i in S:
    b_i=b_list[i]
    if b_i in [1, 2]:
        X = {j for j in S if j != i}
        x=np.array([u[i] for i in sorted(X)]) if X!=0 else 0
        print('x= ', x)
        Xi={i}
        print('Xi= ', Xi)
        xi=x[list(sorted(X)).index(i)] if len(x)>1 else x
        print('xi= ', xi)
        if len(X)==0:
            X=set()
        print('X =', X)
    elif b_i == 0:
        X = {j for j in S if j != i and b_list[j] in [0, 2]}
        x=np.array([u[i] for i in sorted(X)]) if X!=0 else 0
        print('x= ', x)
        Xi={i}
        print('Xi= ', Xi)
        xi=x[list(sorted(X)).index(i)] if len(x)>1 else x
        print('xi= ', xi)
        if len(X)==0:
            X=set()
        print('X =', X)
Y=S-X
for i in Y:
    y=np.array([u[i] for i in sorted(Y)]) if Y!=0 else 0
    print('y= ', y)
    Yi={i}
    print('Yi= ', Yi)
    yi=y[list(sorted(Y)).index(i)] if len(y)>1 else y
    print('xi= ', yi)
    if Y==0 or len(Y)==0:
        Y=0
    print('Y= ', Y)
N_all=int(input('Number of all channels ',))
N=int(input('Number of channels used '))
power=float(input('Power consumption '))
bits=float(input('bits '))
seconds=float(input('seconds '))
fs=float(input('sampling rate '))
length=float(input('length '))
width=float(input('width '))
height=float(input('height '))
material=float(input('material '))
Tsize=length*width*height
length_max=25
width_max=20
height_max=3
wt=Tsize*material/1000
print('weight g', wt)
n=1
if N/10 >0:
    order_of_magnitude = math.floor(math.log10(N))
    scale_factor = 10.0 ** order_of_magnitude
else:
    scale_factor = 1.0
# 1. Полный объем данных, проходящих через используемые каналы (бит/сек)
total_bits_per_sec = fs * scale_factor * bits * N

# 2. Энергетическая стоимость передачи: сколько милливатт уходит на 1 бит/сек
# (чистая физическая метрика: мощность / поток данных)
if total_bits_per_sec > 0:
    energy_per_bit = power / total_bits_per_sec
else:
    energy_per_bit = 0.0

# 3. Учет физического веса через удельную плотность на канал
weight_factor = wt / max(N, 1)

# 4. Интегральная стоимость системы (чем меньше этот показатель, тем эффективнее чип)
system_cost = energy_per_bit * weight_factor

# 5. Естественное преобразование стоимости в эффективность (обратная величина):
# Чем ниже издержки на бит и вес, тем выше итоговый коэффициент e_t,
# который за счет инверсии естественно стремится к диапазону [0, 1)
if system_cost > 0:
    e_t = 1.0 / (1.0 + system_cost * 1e6)  # масштабный множитель здесь отражает физическую размерность мВт/бит
else:
    e_t = 0.0
print('e_t = ', e_t)
e_t_max=1.0
from itertools import combinations
M_list = sorted(list(M))
Z_list = sorted(list(Z))
Theta_big_MZ = []
if len(M_list) > 1 and len(Z_list) > 1:
    for split in range(1, len(M_list)):
        M1 = set(M_list[:split])
        M2 = set(M_list[split:])
        for r in range(1, len(Z_list)):
            for Z1_tuple in combinations(Z_list, r):
                Z1 = set(Z1_tuple)
                Z2 = set(Z_list) - Z1
                Theta_big_MZ.append(((M1, Z1), (M2, Z2)))
print('Theta_big_MZ= ', Theta_big_MZ)
if Theta_big_MZ:
    theta = Theta_big_MZ[0]
else:
    theta = ((set(M_list), set(Z_list)), (set(), set()))
print('theta= ', theta)
P_signal=(e_t/e_t_max)
print('P signal= ', P_signal)
k=10
Omega=2
p_noise_val=1-P_signal
print('p noise val= ',  p_noise_val)
p_noise_total=p_noise_val*(1/Omega**set_number)
print('p_noise_total= ', p_noise_total)
p_total=P_signal + p_noise_total
Omega_Zi=[[]] if (Zi==0 or len(Zi)==0) else list(itertools.product([0.1], repeat=len(Zi)))
Omega_X=[[]] if (X==0 or len(X)==0) else list(itertools.product([0,1], repeat=len(X)))
print('Omega X= ', Omega_X)
tpm_bci_list = []
for x in Omega_X:
    if X == 0 or len(X) == 0:
        mx = np.array(m)
    else:
        mx = np.concatenate([m, x])
        print('mx= ', mx)
    b_weights = np.array([b_list.get(k, 1) for k in range(len(mx))])
    bias = np.random.uniform(0, 1) # bias — это скалярное смещение для узла zi
    signal = (np.dot(b_weights, mx) * zi) + bias# Скалярный суммарный потенциал воздействия  # На выходе 1 число!
    tpm_prob = 1 / (1 + np.exp(-k * signal))
    tpm_bci = (P_signal * tpm_prob) + (p_noise_val*0.5)
    print('tpm bci= ', tpm_bci)
    tpm_bci_list.append(tpm_bci)
    tpm_bci_array = np.array(tpm_bci_list)
    sum_tpm_bci = np.sum(tpm_bci_array)
print('Sum of tpm_bci= ', sum_tpm_bci)
p_e=(1/len(Omega_X))*sum_tpm_bci
print('pe= ', p_e)

Omega_S=list(itertools.product([0,1], repeat=len(S))) if len(S)>0 else [[]]
Omega_S_hat=list(itertools.product([0,1], repeat=len(S_hat))) if len(S)>0 else [[]]
if len(W)>0:
    Omega_W=list(itertools.product([0,1], repeat=len(W)))
else:
    Omega_W=[()]
u_hat=np.array([u[i] for i in range(set_number)])
T_e_bci_list = []              
for s_bar in Omega_S:
    if S == 0 or len(S) == 0:
        sw = np.array(w)
    else:
        sw = np.concatenate([np.atleast_1d(s), np.atleast_1d(w)])
        print('sw= ', sw)
    b_weights = np.array([b_list.get(k, 1) for k in range(len(sw))])
    bias = np.random.uniform(0, 1) # bias — это скалярное смещение для узла zi
    signal = (np.dot(b_weights, sw) * np.array(s_bar)) + bias# Скалярный суммарный потенциал воздействия  # На выходе 1 число!
    T_e = 1 / (1 + np.exp(-k * signal))
    T_e_bci = (P_signal * T_e) + (p_noise_val*0.5)
    print('Te bci= ', T_e_bci)
    T_e_bci_list.append(T_e_bci)
    T_e_bci_array = np.array(T_e_bci_list) 
T_e=T_e_bci_array 
print(T_e)
def T_c(s, s_bar, u):
    total_sum=[]
    current_sum=0
    for w_bar in Omega_W:
        s_hat_w_bar_list = []
        for s_bar in Omega_S:
            if S==0 or len(S)==0:
                s_hat_w_bar=np.atleast_1d(w_bar)
            else:
                s_hat_w_bar = np.concatenate([np.atleast_1d(s_hat), np.atleast_1d(w_bar)])
                
            b_weights = np.array([b_list.get(k, 1) for k in range(len(s_hat_w_bar))])
            bias = np.random.uniform(0, 1)
            signal = (np.dot(b_weights, s_hat_w_bar) * u) + bias
            s_hat_w_bar = 1 / (1 + np.exp(-k * signal))
            s_hat_w_bar_bci = (P_signal * s_hat_w_bar) + (p_noise_val*0.5)
            s_hat_w_bar_list.append(s_hat_w_bar_bci)
            s_hat_w_bar_array = np.array(s_hat_w_bar_list)
            sums_hat_w_bar=np.sum(s_hat_w_bar_array)
            total_sum=np.sum(sums_hat_w_bar)
            
        u_hat_u_list=[]
        for s_bar in Omega_S:
            if S==0 or len(S)==0:
                u =np.array(u_hat)
            else:
                u_hat
                
            b_weights = np.array([b_list.get(k, 1) for k in range(len(u_hat))])
            bias = np.random.uniform(0, 1) 
            signal = (np.dot(b_weights, u_hat) * u) + bias
            u_hat_u = 1 / (1 + np.exp(-k * signal))
            u_hat_u_bci = (P_signal * u_hat_u) + (p_noise_val*0.5)
            u_hat_u_list.append(u_hat_u_bci)
            u_hat_u_array = np.array(u_hat_u_list)
            sums_u_hat_u=np.sum(u_hat_u_array)
            partition=(sums_hat_w_bar)/(sums_u_hat_u)
            current_sum+=partition
            total_sum=np.sum(current_sum)
            
        s_bar_w_bar_list = []
        for s_bar in Omega_S:
            if S==0 or len(S)==0:
                s_bar_w_bar=np.atleast_1d(w_bar)
            else:
                s_bar_w_bar = np.concatenate([np.atleast_1d(s_bar), np.atleast_1d(w_bar)])
                
            b_weights = np.array([b_list.get(k, 1) for k in range(len(s_bar_w_bar))])
            bias = np.random.uniform(0, 1) 
            signal = (np.dot(b_weights, s_bar_w_bar) * si) + bias
            s_bar_w_bar = 1 / (1 + np.exp(-k * signal))
            s_bar_w_bar_bci = (P_signal * s_bar_w_bar) + (p_noise_val*0.5)
            s_bar_w_bar_list.append(s_bar_w_bar_bci)
            s_bar_w_bar_array = np.array(s_bar_w_bar_list)
            sums_bar_w_bar=np.sum(s_bar_w_bar_array)
            total_sum=np.sum(sums_bar_w_bar)
        for i in range(len(S)):
            T_c_result = np.prod(total_sum)
        print('Tc= ', T_c_result)
        return T_c_result
p_e_s_bar_s_list=[]
for s in Omega_S:
    s_bar=np.array(s_bar, dtype=float)
    if S==0 or len(S)==0:
        p_e_s_bar_s=np.atleast_1d(s)
    else:
        p_e_s_bar_s = s
    b_weights = np.array([b_list.get(k, 1) for k in range(len(p_e_s_bar_s))])
    bias = np.random.uniform(0, 1) 
    signal = (np.dot(b_weights, p_e_s_bar_s) * s_bar) + bias
    p_e_s_bar_s = 1 / (1 + np.exp(-k * signal))
    p_e_s_bar_s_bci = (P_signal * p_e_s_bar_s) + (p_noise_val*0.5)
    p_e_s_bar_s_list.append(p_e_s_bar_s_bci)
    p_e_s_bar_s_array = np.array(p_e_s_bar_s_list)
    sums_p_e_s_bar_s=np.sum(p_e_s_bar_s_array)
    p_e_s_bar=(1/len(Omega_S))*sums_p_e_s_bar_s
print('p_e_s_bar= ', p_e_s_bar)
p_e_s_bar_s_list=[]
for s_bar in Omega_S:
    s=np.array(s, dtype=float)
    if S==0 or len(S)==0:
        p_e_s_bar_s=np.atleast_1d(s_bar)
    else:
        p_e_s_bar_s = s_bar
    b_weights = np.array([b_list.get(k, 1) for k in range(len(p_e_s_bar_s))])
    bias = np.random.uniform(0, 1) 
    signal = (np.dot(b_weights, p_e_s_bar_s) * s) + bias
    p_e_s_bar_s = 1 / (1 + np.exp(-k * signal))
    p_e_s_bar_s_bci = (P_signal * p_e_s_bar_s) + (p_noise_val*0.5)
    p_e_s_bar_s_list.append(p_e_s_bar_s_bci)
    p_e_s_bar_s_array = np.array(p_e_s_bar_s_list)
    sums_p_e_s_bar_s=np.sum(p_e_s_bar_s_array)
    p_e_s=(1/len(Omega_S))*sums_p_e_s_bar_s
print('p_e_s= ', p_e_s)

sum_T_c=0
for s_bar in Omega_S:
    sum_T_c=np.sum(T_c(s=s, s_bar=s_bar, u=u))
    target_sum_Tc = np.sum(T_c(s=s, s_bar=s_bar, u=u))
    p_c_s=(1/len(Omega_S))*sum_T_c
print('p_c_s= ', p_c_s)

def p_c_barckwards_s_bar_s(s_bar, s):
    T_c_sum=0.0
    for s_hat in Omega_S:
        T_c_sum+=(T_c(s=s, s_bar=s_hat, u=u))
        print('T_c_sum= ', T_c_sum)
    p_c_barckwards_s_bar_s=T_c(s=s, s_bar=s_bar, u=u)/T_c_sum
    print('p_c_barckwards_s_bar_s= ', p_c_barckwards_s_bar_s)
    return p_c_barckwards_s_bar_s
ii_e_s_s_bar_list=[]
for s in Omega_S:
    log_1=np.log2(p_e_s_bar_s/p_e_s_bar)
    print('log_1= ', log_1)
    ii_e_s_s_bar=p_e_s_bar_s*log_1
    print('ii_s_s_bar= ', ii_e_s_s_bar)
    ii_e_s_s_bar_list.append(ii_e_s_s_bar)
s_e_all_T_e_s=np.argmax(ii_e_s_s_bar_list)
print('s_e_all_T_e_s= ', s_e_all_T_e_s)

ii_c_s_s_bar_list=[]
for s in Omega_S:
    log_2=np.log2(T_c(s=s, s_bar=s_bar, u=u)/p_c_s)
    print('log_2= ', log_2)
    if log_2>0:
        ii_c_s_s_bar=p_c_barckwards_s_bar_s(s_bar, s)*log_2
        print('ii_c_s_s_bar= ', ii_c_s_s_bar)
    else:
        ii_c_s_s_bar=0
    ii_c_s_s_bar_list.append(ii_c_s_s_bar)
best_idx = np.argmax(ii_c_s_s_bar_list)
s_c_all_T_c_s = Omega_S[best_idx]
print('s_c_all_T_c_s= ', s_c_all_T_c_s)
    
s_bar_j=float(s_bar[0])*j
print('s_bar_j= ', s_bar_j)
Omega_Xi=[[]] if (Xi==0 or len(Xi)==0) else list(itertools.product([0.1], repeat=len(Xi)))
p_e_sj_xy_list=[]
for xi in Omega_Xi:
    if Xi==0 or len(Xi)==0:
        xiyi=np.array(yi)
    else:
        xiyi = np.concatenate([np.atleast_1d(xi), np.atleast_1d(yi)])
        print('xiyi= ', xiyi)
    b_weights = np.array([b_list.get(k, 1) for k in range(len(xiyi))])
    bias = np.random.uniform(0, 1) 
    signal = (np.dot(b_weights, xiyi) * s_bar_j) + bias
    p_e_sj_xy = 1 / (1 + np.exp(-k * signal))
    p_e_sj_xy_bci = (P_signal * p_e_sj_xy) + (p_noise_val*0.5)
    p_e_sj_xy_list.append(p_e_sj_xy_bci)
    p_e_sj_xy_array = np.array(p_e_sj_xy_list)
sum_p_e_sj_xy=np.sum(p_e_sj_xy_array)
p_e_theta_sjs=(1/len(Omega_Xi))*sum_p_e_sj_xy
print('p_e_theta_sjs= ', p_e_theta_sjs)

p_e_s_e_all_s_list=[]
for s in Omega_S:
    p_e_s_e_all_s = np.array(p_e_s_e_all_s) if S==0 or len(S)==0 else np.concatenate([np.atleast_1d(s), np.atleast_1d(s_e_all_T_e_s)])
    b_weights = np.array([b_list.get(k, 1) for k in range(len(s))])
    bias = np.random.uniform(0, 1) 
    signal = (np.dot(b_weights, s) * s_e_all_T_e_s) + bias
    p_e_s_e_all_s = 1 / (1 + np.exp(-k * signal))
    p_e_s_e_all_s_bci = (P_signal * p_e_s_e_all_s) + (p_noise_val*0.5)
    p_e_s_e_all_s_list.append(p_e_s_e_all_s_bci)
    p_e_s_e_all_s_array = np.array(p_e_s_e_all_s_list)
print('p_e_s_e_all_s= ', p_e_s_e_all_s_array)

p_e_theta_s_e_all_s_list =[]
for xi in Omega_Xi:
    p_e_theta_s_e_all_s = np.array(s_e_all_T_e_s) if S==0 or len(S)==0 else np.concatenate([np.atleast_1d(s), np.atleast_1d(s_e_all_T_e_s)])
    b_weights = np.array([b_list.get(k, 1) for k in range(len(s))])
    bias = np.random.uniform(0, 1) 
    signal = (np.dot(b_weights, s) * s_e_all_T_e_s) + bias
    p_e_theta_s_e_all_s = 1 / (1 + np.exp(-k * signal))
    p_e_theta_s_e_all_s_bci = (P_signal * p_e_theta_s_e_all_s) + (p_noise_val*0.5)
    p_e_theta_s_e_all_s_list.append(p_e_theta_s_e_all_s_bci)
    p_e_theta_s_e_all_s_array = np.array(p_e_theta_s_e_all_s_list)
print('p_e_theta_s_e_all_s= ', p_e_theta_s_e_all_s_array)

phi_e_T_e_s_theta=p_e_s_e_all_s_array.flatten(order='C')*np.maximum(0, np.log2(p_e_s_e_all_s_array/p_e_theta_s_e_all_s_array))
print('phi_e_T_e_s_theta= ', phi_e_T_e_s_theta)

s_c_all_T_c_s_list=[]
for s in Omega_S:
    s_c_all_T_c_s = np.array(s_c_all_T_c_s) if S==0 or len(S)==0 else np.concatenate([np.atleast_1d(float(s[0])), np.atleast_1d(s_c_all_T_c_s)])
    b_weights = np.array([b_list.get(k, 1) for k in range(len(s_c_all_T_c_s))])
    bias = np.random.uniform(0, 1) 
    signal = (np.dot(b_weights, s_c_all_T_c_s) * float(s[0])) + bias
    s_c_all_T_c_s = 1 / (1 + np.exp(-k * signal))
    s_c_all_T_c_s_bci = (P_signal * s_c_all_T_c_s) + (p_noise_val*0.5)
    s_c_all_T_c_s_list.append(s_c_all_T_c_s_bci)
    s_c_all_T_c_s_array = np.array(s_c_all_T_c_s_list)
print('p_c_s_c_all_s= ', s_c_all_T_c_s_array)

s_c_theta_T_c_s_list=[]
for xi in Omega_Xi:
    s_c_theta_T_c_s = np.array(s_c_all_T_c_s) if S==0 or len(S)==0 else np.concatenate([np.atleast_1d(float(s[0])), np.atleast_1d(s_c_all_T_c_s)])
    b_weights = np.array([b_list.get(k, 1) for k in range(len(s_c_theta_T_c_s))])
    bias = np.random.uniform(0, 1) 
    signal = (np.dot(b_weights, s_c_all_T_c_s) * float(s[0])) + bias
    s_c_theta_T_c_s= 1 / (1 + np.exp(-k * signal))
    s_c_theta_T_c_s_bci = (P_signal * s_c_theta_T_c_s) + (p_noise_val*0.5)
    s_c_theta_T_c_s_list.append(s_c_theta_T_c_s_bci)
    s_c_theta_T_c_s_array = np.array(s_c_theta_T_c_s_list).flatten(order='C')
print('p_c_s_c_theta_s= ', s_c_theta_T_c_s_array.flatten(order='C'))

p_c_s_c_all_s=p_c_barckwards_s_bar_s(s_bar=s_c_all_T_c_s, s=s)
print('s bar & s_c_all_T_c_s= ', s_bar, s_c_all_T_c_s)
print('p_c_s_c_all_s= ', p_c_s_c_all_s)

s_c_theta_aligned = np.tile(s_c_theta_T_c_s_array, len(s_c_all_T_c_s_array) // len(s_c_theta_T_c_s_array))
phi_c_T_c_s_theta=p_c_s_c_all_s*np.maximum(0, np.log(s_c_all_T_c_s_array/s_c_theta_aligned))
print('phi_c_T_c_s_theta= ', phi_c_T_c_s_theta)

phi_s_T_e_T_c_s_theta=np.minimum(phi_c_T_c_s_theta, phi_e_T_e_s_theta)
print('phi_s_T_e_T_c_s_theta= ', phi_s_T_e_T_c_s_theta)

sum_phi_s_T_all_e_T_all_c_s_theta=0
for theta in Theta_big_MZ:
    k_part=len(theta)
    print(f"Часть {i+1}: Si={Si} (длина {len(Si)}), Xi={Xi} (длина {len(Xi)})")
    sum_phi_s_T_all_e_T_all_c_s_theta=sum(len(Si)*len(Xi) for Si, Xi in theta)
print('phi_s_T_all_e_T_all_c_s_theta= ', sum_phi_s_T_all_e_T_all_c_s_theta)

Omega_Z=list(itertools.product([0,1], repeat=len(Z))) if len(Z)>0 else [[]]
i=1
pi_e_z_m_list=[]
for z in Omega_Z:
    for i in range(len(Z)+1):
        if Z==0 or len(Z)==0:
            pi_e_z_m =np.atleast_1d(m)
        else:
            pi_e_z_m_val = np.array(m)
    
        b_weights = np.array([b_list.get(k, 1) for k in range(len(pi_e_z_m_val))])
        bias = np.random.uniform(0, 1) 
        signal = (np.dot(b_weights, zi) * np.array(m)) + bias
        pi_e_z_m = 1 / (1 + np.exp(-k * signal))
        pi_e_z_m_bci = (P_signal * pi_e_z_m) + (p_noise_val*0.5)
        pi_e_z_m_list.append(pi_e_z_m_bci)
        pi_e_z_m_array = np.array(pi_e_z_m_list)
        pi_e_z_m_prod = np.prod(pi_e_z_m_array)
    pi_e_z_m=pi_e_z_m_prod
print('pi_e_z_m= ', pi_e_z_m)

Omega_M=list(itertools.product([0,1], repeat=len(M))) if len(M)>0 else [[]]
i=1
pi_c_m_z_list=[]
for m in Omega_M:
    for i in range(len(M)+1):
        if M==0 or len(M)==0:
            pi_c_m_z =np.atleast_1d(z)
        else:
            pi_c_m_z_val = np.array(z)
        b_weights = np.array([b_list.get(k, 1) for k in range(len(pi_c_m_z_val))])
        bias = np.random.uniform(0, 1) 
        signal = (np.dot(b_weights, mi) * np.array(z)) + bias
        pi_c_m_z = 1 / (1 + np.exp(-k * signal))
        pi_c_m_z_bci = (P_signal * pi_c_m_z) + (p_noise_val*0.5)
        pi_c_m_z_list.append(pi_c_m_z_bci)
        pi_c_m_z_array = np.array(pi_c_m_z_list)
        pi_c_m_z_prod = np.prod(pi_c_m_z_array)
pi_c_m_z=pi_c_m_z_prod
print('pi_c_m_z= ', pi_c_m_z)

for z in Omega_Z:
    for m in Omega_M:
        pi_e_z_M_sum=np.sum(pi_e_z_m)
        pi_e_z_M=(1/len(Omega_M))*pi_e_z_M_sum
print('pi_e_z_M= ', pi_e_z_M)

for m in Omega_M:
    for z in Omega_Z:
        pi_c_m_Z_sum=np.sum(pi_c_m_z)
        pi_e_m_Z=(1/len(Omega_Z))*pi_c_m_Z_sum
print('pi_e_m_Z= ', pi_e_m_Z)

Omega_Y=list(itertools.product([0,1], repeat=len(Y))) if len(Y)>0 else [[]]

def p_c_mi_zy(mi, z):
    p_c_mi_zy_list=[]
    for y in Omega_Y:
        if Y==0 or len(Y)==0:
            zy=np.atleast_1d(z)
        else:
            zy = np.concatenate([np.atleast_1d(z), np.atleast_1d(y)])
        b_weights = np.array([b_list.get(k, 1) for k in range(len(zy))])
        bias = np.random.uniform(0, 1) 
        signal = (np.dot(b_weights, zy) * np.array(mi)) + bias
        p_c_mi_zy = 1 / (1 + np.exp(-k * signal))
        p_c_mi_zy_bci = (P_signal * p_c_mi_zy) + (p_noise_val*0.5)
        p_c_mi_zy_list.append(p_c_mi_zy_bci)
        p_c_mi_zy_array = np.array(p_c_mi_zy_list)
        sums_p_e_s_bar_s=np.sum(p_c_mi_zy_array)
    p_c_mi_zy=(1/len(Omega_Y))*np.sum(p_c_mi_zy_array)
    print('p_c_mi_zy= ', p_c_mi_zy)
    return p_c_mi_zy
p_c_mi_z_hat=p_c_mi_zy(mi=mi, z=z_hat)
print('p_c_mi_z_hat= ', p_c_mi_z_hat)

i=1
p_c_mi_zy_list_2=[]
for i in range(len(M)):
    value=p_c_mi_zy(mi=mi, z=z)
    p_c_mi_zy_list_2.append(value)
p_c_mi_zy_prod=np.prod(p_c_mi_zy_list_2)
print('p_c_mi_zy_prod= ', p_c_mi_zy_prod)  

i=1
for z_hat in Omega_Z:
    p_c_mi_z_hat_list_2=[]
    for i in range(len(M)):
        value=p_c_mi_zy(mi=mi, z=z_hat)
        p_c_mi_z_hat_list_2.append(value)
    p_c_mi_z_hat_prod=np.prod(p_c_mi_z_hat_list_2)
    p_c_mi_z_hat_prod_sum=np.sum(p_c_mi_z_hat_prod)
print('p_c_mi_z_hat_prod= ', p_c_mi_z_hat_prod)
print('p_c_mi_z_hat_prod_sum= ', p_c_mi_z_hat_prod_sum)

def pi_c_backwards_z_m(z,m):
    pi_c_backwards_z_m=np.clip(p_c_mi_zy_prod/p_c_mi_z_hat_prod_sum, 0.0, 1.0)
    print('pi_c_backwards_z_m= ', pi_c_backwards_z_m)
    return pi_c_backwards_z_m

ii_e_m_z_list=[]
for z in Omega_Z:
    ii_e_m_z=pi_e_z_m*np.log2(pi_e_z_m/pi_e_z_M)
    print('ii_e_m_z= ', ii_e_m_z)
    ii_e_m_z_list.append(ii_e_m_z)
    ii_e_m_z_array=np.array(ii_e_m_z_list)
    z_e_all_m_Z=np.max(ii_e_m_z_array)
    z_e_all_m_Z_max=np.argmax(ii_e_m_z_array)
    print('z_e_all_m_Z= ', z_e_all_m_Z_max)

ii_c_m_z_list=[]
for m in Omega_M:
    ii_c_m_z=pi_c_backwards_z_m(z=z,m=m)*np.log2(pi_c_m_z/pi_e_m_Z)
    print('ii_c_m_z= ', ii_c_m_z)
    ii_c_m_z_list.append(ii_c_m_z)
    ii_c_m_z_array=np.array(ii_c_m_z_list)
    z_c_all_M_z=np.max(ii_c_m_z_array)
    z_c_all_M_z_max=np.argmax(ii_c_m_z_array)
    print('z_c_all_M_z= ', z_c_all_M_z_max)

sum_phi_s_T_all_e_T_all_c_s_theta=0
for theta in Theta_big_MZ:
    k=len(theta)
    print(f"Часть {i+1}: Si={Si} (длина {len(Si)}), Xi={Xi} (длина {len(Xi)})")
    sum_phi_s_T_all_e_T_all_c_s_theta=sum(len(Mi)*len(Zi) for Mi, Zi in theta)
print('phi_s_T_all_e_T_all_c_s_theta= ', sum_phi_s_T_all_e_T_all_c_s_theta)

pi_e_theta_z_e_all_m_list =[]
for z_e_all in Omega_Z:
    z_e_all_i=z_e_all
    print('z_e_all_i= ', z_e_all_i)
    for theta in Theta_big_MZ:
        k_part=len(theta)
        
        pi_e_theta_z_e_all_m_val = np.array(z_e_all_i) if Mi==0 or len(Mi)==0 else np.concatenate([np.atleast_1d(z_e_all_i), np.atleast_1d(mi)])
        b_weights = np.array([b_list.get(k, 1) for k in range(len(z_e_all_i))])
        bias = np.random.uniform(0, 1) 
        signal = (np.dot(b_weights, z_e_all_i) * mi) + bias
        pi_e_theta_z_e_all_m = 1 / (1 + np.exp(-k * signal))
        pi_e_theta_z_e_all_m_bci = (P_signal * pi_e_theta_z_e_all_m) + (p_noise_val*0.5)
        pi_e_theta_z_e_all_m_list.append(pi_e_theta_z_e_all_m_bci)
        pi_e_theta_z_e_all_m_array = np.array(pi_e_theta_z_e_all_m_list)
        pi_e_theta_z_e_all_m=pi_e_theta_z_e_all_m_array
        print('pi_e_theta_z_e_all_m= ', pi_e_theta_z_e_all_m)
pi_e_z_all_e_m_list=[]
for z in Omega_Z:
    if Z==0 or len(Z)==0:
        pi_e_z_all_e_m_val=m
    else:
        pi_e_z_all_e_m_val = np.concatenate([np.atleast_1d(z_e_all_m_Z), np.atleast_1d(m)])
        print('pi_e_z_all_e_m_val= ', pi_e_z_all_e_m_val)
    b_weights = np.ones(len(pi_e_z_all_e_m_val))
    print('b_weights= ', b_weights)
    bias = np.random.uniform(0, 1)
    signal = np.dot(b_weights, pi_e_z_all_e_m_val) + bias
    pi_e_z_all_e_m = 1 / (1 + np.exp(-k * signal))
    pi_e_z_all_e_m_bci = (P_signal * pi_e_z_all_e_m) + (p_noise_val*0.5)
    pi_e_z_all_e_m_list.append(pi_e_z_all_e_m_bci)
    pi_e_z_all_e_m_array = np.array(pi_e_z_all_e_m_list)
    pi_e_z_all_e_m=pi_e_z_all_e_m_array
    print('pi_e_z_all_e_m= ', pi_e_z_all_e_m)

num_states=len(pi_e_z_all_e_m)
if len(pi_e_z_all_e_m)!=num_states:
    temp_array=np.array(pi_e_theta_z_e_all_m)
    reshaped_array=temp_array.reshape(num_states, -1)
    pi_e_theta_z_e_all_m=np.mean(reshaped_array, axis=1)


num_states=len(pi_e_z_all_e_m)
pi_e_theta_z_e_all_m = np.full(num_states, 1.0 / num_states)
def phi_e_m_Z_theta(m,Z,theta,pi_e_theta_z_e_all_m):
    num_states=len(pi_e_z_all_e_m)
    phi_e_m_Z_theta =pi_e_z_all_e_m.flatten(order='C')*np.maximum(0, np.log2(pi_e_z_all_e_m/pi_e_theta_z_e_all_m))
    print('phi_e_m_Z_theta= ', phi_e_m_Z_theta)
    return phi_e_m_Z_theta
pi_e_theta_z_e_all_m = np.full(len(pi_e_z_all_e_m), 1.0 / len(pi_e_z_all_e_m))
phi_c_m_Z_theta=phi_e_m_Z_theta(m=z,Z=M,theta=theta,pi_e_theta_z_e_all_m=pi_e_theta_z_e_all_m)
print('phi_c_m_Z_theta= ', phi_c_m_Z_theta)

phi_dict = {}
phi_val = np.array([0.0])

for theta in Theta_big_MZ:
    phi_val = np.minimum(phi_c_m_Z_theta, phi_e_m_Z_theta(m, Z, theta, pi_e_theta_z_e_all_m))
    theta_frozen = tuple((frozenset(Mi), frozenset(Zi)) for Mi, Zi in theta)
    phi_dict[theta_frozen] = np.array(phi_val)

phi_max_value = np.max(list(phi_dict.values())) if phi_dict else np.max(phi_val)

# theta' — argmin отношения φ/max(φ)
if phi_max_value > 0 and phi_dict:
    theta_all = min(phi_dict, key=lambda t: np.max(phi_dict[t]) / phi_max_value)
else:
    theta_all = 0

print('all= ', theta_all)

pi_c_m_z_c_all_val_list=[]
for m in Omega_M:
    if M==0 or len(M)==0:
        pi_c_m_z_c_all_val=np.atleast_1d(z_c_all_M_z)
    else:
        pi_c_m_z_c_all_val = np.array(z_c_all_M_z)
    print('pi_c_m_z_c_all_val= ', pi_c_m_z_c_all_val)
    b_weights = np.ones(len(np.atleast_1d(pi_c_m_z_c_all_val)))
    bias = np.random.uniform(0, 1) 
    signal = (np.dot(b_weights, pi_c_m_z_c_all_val) * np.array(m)) + bias
    pi_c_m_z_c_all_val = 1 / (1 + np.exp(-k * signal))
    pi_c_m_z_c_all_val_bci = (P_signal * pi_c_m_z_c_all_val) + (p_noise_val*0.5)
    pi_c_m_z_c_all_val_list.append(pi_c_m_z_c_all_val_bci)
    pi_c_m_z_c_all_val_array = np.array(pi_c_m_z_c_all_val_list)
pi_c_m_z_c_all=pi_c_m_z_c_all_val_array
print('pi_c_m_z_c_all=', pi_c_m_z_c_all)

pi_c_theta_all_m_z_c_all_list=[]
for pi_c_theta_all_z_c_all in Omega_M:
    for theta in Theta_big_MZ:
        k_part=len(theta)
        pi_c_theta_all_m_z_c_all_list=[]
        pi_c_theta_all_m_z_c_all_val = np.array(pi_c_theta_all_z_c_all) if Mi==0 or len(Mi)==0 else np.concatenate([np.atleast_1d(pi_c_theta_all_z_c_all), np.atleast_1d(m)])
        b_weights = np.ones(len(np.atleast_1d(pi_c_theta_all_m_z_c_all_val)))
        bias = np.random.uniform(0, 1) 
        signal = (np.dot(b_weights, pi_c_theta_all_m_z_c_all_val) * np.array(m)) + bias
        pi_c_theta_all_m_z_c_all = 1 / (1 + np.exp(-k * signal))
        pi_c_theta_all_m_z_c_all_bci = (P_signal * pi_c_theta_all_m_z_c_all) + (p_noise_val*0.5)
        pi_c_theta_all_m_z_c_all_list.append(pi_c_theta_all_m_z_c_all_bci)
        pi_c_theta_all_m_z_c_all_array = np.array(pi_c_theta_all_m_z_c_all_list)
        pi_c_theta_all_m_z_c_all=pi_c_theta_all_m_z_c_all_array
        print('pi_c_theta_all_m_z_c_all= ', pi_c_theta_all_m_z_c_all)

pi_c_backwards_z_c_all_m=pi_c_backwards_z_m(z=z_c_all_M_z,m=m)
print('pi_c_backwards_z_c_all_m= ', pi_c_backwards_z_c_all_m)

def phi_e_m_z_e_all(m,Z):
    phi_e_m_z_e_all=phi_e_m_Z_theta(m=m,Z=z_e_all_m_Z,theta=0,pi_e_theta_z_e_all_m=pi_e_theta_z_e_all_m)
    print('phi_e_m_z_e_all= ', phi_e_m_z_e_all)
    return phi_e_m_z_e_all

phi_c_m_z_e_all=phi_e_m_z_e_all(m=z,Z=M)
print('phi_c_m_z_e_all = ', phi_c_m_z_e_all) 

for Z in S:
    z_e_ALL_m=np.argmax(phi_e_m_z_e_all(m=m,Z=Z))
    print('z_e_ALL_m= ', z_e_ALL_m)
for Z in S:
    phi_e_m=phi_e_m_z_e_all(m=m,Z=Z)[z_e_ALL_m]
print('phi_e_m= ', phi_e_m)

for Z in S:
    z_c_ALL_m=np.argmax(phi_c_m_z_e_all)
    print('z_e_ALL_m= ', z_e_ALL_m)
for Z in S:
    phi_c_m=phi_c_m_z_e_all[z_c_ALL_m]
print('phi_c_m= ', phi_c_m)

phi_d_m=np.minimum(phi_c_m, phi_e_m)
print('phi_d_m =', phi_d_m)

z_c_ALL = Omega_Z[z_c_ALL_m]
z_e_ALL = Omega_Z[z_e_ALL_m]
z_ALL={z_c_ALL, z_e_ALL}
print('z_ALL =', z_ALL)


d_m=(m, z_ALL, float(phi_d_m))
print('d_m= ', d_m)

s_c_all_T_c_s = np.atleast_1d(s_c_all_T_c_s)  # превращаем в массив
s_e_all_T_e_s = np.atleast_1d(s_e_all_T_e_s)
D_T_e_T_c_s=[]
for z_c_ALL_m in s_c_all_T_c_s:
    for z_e_ALL_m in s_e_all_T_e_s:
        for m in s:
            if phi_d_m>0:
                z_c_set = set(np.atleast_1d(z_c_ALL_m))
                z_e_set = set(np.atleast_1d(z_e_ALL_m))
                s_c_set = set(np.atleast_1d(s_c_all_T_c_s))
                s_e_set = set(np.atleast_1d(s_e_all_T_e_s))
                if z_c_set <= s_c_set and z_e_set <= s_e_set:
                    d_new = (m, (z_c_ALL_m, z_e_ALL_m), float(phi_d_m))
                    D_T_e_T_c_s.append(d_new)
                    print('D_T_e_T_c_s= ', D_T_e_T_c_s)
d_fat = D_T_e_T_c_s  # сам список различий
print('d_fat= ', d_fat)
print('|d_fat|= ', len(d_fat)) 

all_purviews=[]
z_fat = []
all_z = []
for d in D_T_e_T_c_s:
    m_d, (z_c_d, z_e_d), phi_d_val = d_new
    z_single = frozenset(np.atleast_1d(z_c_d)) | frozenset(np.atleast_1d(z_e_d))
    all_purviews.append(z_single)
print('all_purviews= ', all_purviews)

for r in range(2, len(all_purviews) + 1):
    for combo in itertools.combinations(all_purviews, r):
        overlap = set.intersection(*[set(z) for z in combo])
        if len(overlap) > 0:  
            z_fat.append(combo)
print('z_fat= ', z_fat)

if len(z_fat) > 0:
    o_ALL_z_fat = set.intersection(*[set.union(*[set(z) for z in combo]) for combo in z_fat])
else:
    o_ALL_z_fat = set()
print('o_ALL_z_fat =', o_ALL_z_fat)

def f_z(z_ALL):
    sets = [set(z) for z in z_ALL]
    if len(sets) > 1:
        o_ALL = set.intersection(*sets)
    else:
        o_ALL = sets[0]
    return (z_ALL, o_ALL)
f_fat_d = [f_z(z) for z in z_fat]
print('f_fat_d= ', f_fat_d)

o_ALL_union = set()
for d in d_fat:
    m_d, (z_c_ALL_d, z_e_ALL_d), phi_d_val = d  # распаковываем d здесь
    for f in f_fat_d:
        z_combo, o_ALL_f = f
        o_ALL_union = o_ALL_union | o_ALL_f

    purview_union = set(np.atleast_1d(z_c_ALL_d)) | set(np.atleast_1d(z_e_ALL_d))
    if len(purview_union) > 0:
        phi_r_d_fat = np.minimum(len(o_ALL_union) * (phi_d_val / len(purview_union)),1)
    else:
        phi_r_d_fat = 0.0
    print('phi_r_d_fat= ', phi_r_d_fat)

R_D=[]
for d_fat in D_T_e_T_c_s:
    r_d_fat = (d_fat, f_fat_d, phi_r_d_fat)
    if phi_r_d_fat>0:
        R_D.append(r_d_fat)
    print('R_D= ', R_D)

C_T_e_T_c_s_ALL = {'distinctions': D_T_e_T_c_s, 'relations': R_D}
print('C_T_e_T_c_s_ALL= ', C_T_e_T_c_s_ALL)

Phi=sum(float(d[2]) for d in D_T_e_T_c_s)+sum(float(r[2]) for r in R_D)
print('Phi= ', Phi)

