from selenium import webdriver
import time

PATH = "C:\Program Files (x86)\chromedriver.exe"
driver = webdriver.Chrome(PATH)

driver.get(
    "https://www.marcusmillichap.com/advisors?type=agent#3070fbfb-aab6-491c-a4aa-ae7a5c8a08abfacet=Advisor%20Type:Agent")

time.sleep(10)
advisor_list = []
advisor_email = []
export_list = []
sub_string = 'advisors/'
sub_string2 = '@marcusmillichap.com'
l = 0

while l < 118:
    try:
        time.sleep(10)
        ids = driver.find_elements_by_xpath('//*[@href]')
        advisor_list.clear()
        for i in ids:
            advisor_list.append(i.get_attribute('href'))
        for i in advisor_list:
            if sub_string in i:
                driver.get(i)
                time.sleep(5)
                irs = driver.find_elements_by_xpath('//*[@href]')
                advisor_email.clear()
                for j in irs:
                    advisor_email.append(j.get_attribute('href'))
                for k in advisor_email:
                    if sub_string2 in k:
                        str_new = k.replace("mailto:","")
                        export_list.append(str_new)
                        break
                    else:
                        continue
    except:
        print(' ')
        print('!!!!!!!exception!!!!!!!')
        print(' ')
        continue
    l = l + 1
    print(l)
    driver.get("https://www.marcusmillichap.com/advisors#70016700-2812-403e-aaf5-ccb34f32635apage=" + str(l))
    driver.implicitly_wait(10)

for r in export_list:
    print(r)

time.sleep(10)
driver.quit()
