import pyfiglet
import websocket
import ssl
import os
import json
import gzip
import requests
from time import sleep
import random
import concurrent.futures

created=0
failed=0


L = '\033[1;33m' #اصفر
C = "\033[1;97m" #ابيض
B = '\033[2;36m'#سمائي
Y = '\033[1;34m' #ازرق فاتح.
C = "\033[1;97m" #ابيض
X = '\037' #ابيض
G = '\033[1;32m'  #أخضر
R = '\033[1;31m' #أحمر

font = pyfiglet.figlet_format('V l P _ Q 1')
print(G+font)
print(Y+"∞"*60)
print(B+'مرحبًا بك في إنشاء حساب لـ SafeUM ')
print(Y+"∞"*60)
id = input(f'{L} ID ⍣⃟ـ𓆪ᬼ𓆪ٱلﻗﻓري𓆩ᬼ𓆩⍣⃟    يقلك حط أيدي حسابك : ')
os.system('clear')

font = pyfiglet.figlet_format('V l P _ Q 2')
print(G+font)
print(Y+"∞"*60)
print(B+'مرحبًا بك في إنشاء حساب لـ SafeUM') 
print(Y+"∞"*60)
token = input(f'{L} Token Bot يقلك ⍣⃟ـ𓆪ᬼ𓆪ٱلﻗﻓري𓆩ᬼ𓆩⍣⃟   حط توكن بوتك: ')
print(Y+"∞"*60)
os.system('clear')

import time 
font = pyfiglet.figlet_format('V l P _ Q 3')
print(G+font)
print(G+"¤"*60)
print(L+"مرحبا في اداة صنع حسابات تطبيق SafeUM")
print(L+"سوف تبدا الاداة في انشاء الحسابات بعد 3ثوان ")
print(G+"¤"*60)
time.sleep(2)


ch='qwertyuioplkjhgfdsazxcvbnm1234567890'
def create():
 global created
 global failed
 user=str(random.choice('qwertyuioplkjhgfdsazxcvbnm')[0])+str(''.join(random.choice(ch) for i in range(7)))
 
 tlg = f'''تم صيد حساب جديد بواسطة ⍣⃟ـ𓆪ᬼ𓆪ٱلﻗﻓري𓆩ᬼ𓆩⍣⃟    لتفعيل تطبيق SafeUM
⋘─────━━─────⋙
˛ U𝗌er  : {user}
˛ 𝖯𝖺𝗌𝗌𝗐𝗈𝗋𝖽 : hhhh
⋘─────━━─────⋙
BY : @VlP_Q1 @VlP_Q2
   '''
 
 #user='kdvdfejevfsheh'
 
 headers = {
     "app": "com.safeum.android",
     "host": None,
     "remoteIp": "134.209.93.148",
     "remotePort": str(8080),
     "sessionId": "b6cbb22d-06ca-41ff-8fda-c0ddeb148195",
     "time": "2023-04-30 12:13:32",
     "url": "wss://51.79.208.190/Auth"
 }
 
 
 data0={"action":"Register","subaction":"Desktop","locale":"en_GB","gmt":"+02","password":{"m1x":"503c73d12b354f86ff9706b2114704380876f59f1444133e62ca27b5ee8127cc","m1y":"6387ae32b7087257452ae27fc8a925ddd6ba31d955639838249c02b3de175dfc","m2":"219d1d9b049550f26a6c7b7914a44da1b5c931eff8692dbfe3127eeb1a922fcf","iv":"e38cb9e83aef6ceb60a7a71493317903","message":"0d99759f972c527722a18a74b3e0b3c6060fe1be3ad53581a7692ff67b7bb651a18cde40552972d6d0b1482e119abde6203f5ab4985940da19bb998bb73f523806ed67cc6c9dbd310fd59fedee420f32"},"magicword":{"m1x":"04eb364e4ef79f31f3e95df2a956e9c72ddc7b8ed4bf965f4cea42739dbe8a4a","m1y":"ef1608faa151cb7989b0ba7f57b39822d7b282511a77c4d7a33afe8165bdc1ab","m2":"4b4d1468bfaf01a82c574ea71c44052d3ecb7c2866a2ced102d0a1a55901c94b","iv":"b31d0165dde6b3d204263d6ea4b96789","message":"8c6ec7ce0b9108d882bb076be6e49fe2"},"magicwordhint":"0000","login":str(user),"devicename":"Xiaomi Redmi Note 8 Pro","softwareversion":"1.1.0.1380","nickname":"hvtctchnjvfxfx","os":"AND","deviceuid":"c72d110c1ae40d50","devicepushuid":"*dxT6B6Solm0:APA91bHqL8wxzlyKHckKxMDz66HmUqmxCPAVKBDrs8KcxCAjwdpxIPTCfRmeEw8Jks_q13vOSFsOVjCVhb-CkkKmTUsaiS7YOYHQS_pbH1g6P4N-jlnRzySQwGvqMP1gxRVksHiOXKKP","osversion":"and_11.0.0","id":"1734805704"}
 
 ws=websocket.create_connection("wss://51.79.208.190/Auth", header=headers, sslopt={"cert_reqs": ssl.CERT_NONE})
 ws.send(json.dumps(data0))
 result=ws.recv()
 decoded_data = gzip.decompress(result)
 #print(G+str(decoded_data))
 if '"comment":"Exists"' in str(decoded_data):
  failed+=1
 elif '"status":"Success"' in str(decoded_data):
  created+=1
  y = requests.post(f"https://api.telegram.org/bot{token}/sendmessage?chat_id={id}&text="+str(tlg))
 elif '"comment":"Retry"' in str(decoded_data):
  failed+=1
 else:
  print(decoded_data)


executor=concurrent.futures.ThreadPoolExecutor(max_workers=500)

while True:
 executor.submit(create)
 os.system('clear')
 font = pyfiglet.figlet_format('V l P _ Q 4')
 print(G+font)
 print(L+"_"*60)
 print(B+"Make free account for safeUM app ")
 print(L+"_"*60)
 print(G+"∞"*60)
 print(G+'Created : '+str(created))
 print(G+"∞"*60)
 print(R+"∞"*60)
 print(R+'Failed : '+str(failed))
 print(R+"∞"*60)
 print(B+"_"*60)
 print(L+"@VlP_Q1/@VlP_Q2")
 print(B+"_"*60)
 print(G+"                                                                 للتواصل معا المطور على واتساب 967711132045+")
 print(R+"يمنع أي سرقة أو تعديل للآداة الخاصة بالجلاد القفري")

 print(B+''' \033[92
 ──▐─▌──▐─▌──
─▐▌─▐▌▐▌─▐▌─
─█▄▀▄██▄▀▄█─
──▄──██▌─▄──
▄▀─█▀██▀█─▀▄
▐▌▐▌─▐▌─▐▌▐▌
─▐─█────█─▌─
────▌──▐────\033[0''')![Screenshot_٢٠٢٤١١٢١-٠٠٠٨٣٣_Pydroid 3](https://github.com/user-attachments/assets/e2295de5-60ab-4499-8eec-72e76d2fd950)
![Screenshot_٢٠٢٤١١٢١-٠٠١٠٥٥_Pydroid 3](https://github.com/user-attachments/assets/51c35bc2-11b2-491b-be08-30aa1c6513b4)
![Screenshot_٢٠٢٤١١٢١-٠٠٢٧٠٧_Pydroid 3](https://github.com/user-attachments/assets/3c6d7e06-be4b-4b08-9f0b-a7035bcfaed7)
![Screenshot_٢٠٢٤١١٢١-٠٠٣٦٤٧_Pydroid 3](https://github.com/user-attachments/assets/c00883e2-976b-47a5-8cb7-fd6da5866392)
