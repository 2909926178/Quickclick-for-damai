# 项目负责人 黄乐成
# 编译环境为python 需要调用selenium插件 个人支持pycharm编译器
from selenium import webdriver  # 操作谷歌浏览器 需要额外安装的 并且现在安装这个模块得指定版本 3.4
from time import sleep
import pickle  # 保存和读取cookie实现免登录的工具
import os   # 操作文件的模块
# 大麦网主页
damai_url = "https://www.damai.cn/"
# 登录页
login_url = "https://passport.damai.cn/login?ru=https%3A%2F%2Fwww.damai.cn%2F"
# 抢票目标页
target_url = "https://detail.damai.cn/item.htm?spm=a2oeg.search_category.0.0.4dfa4d15o9BWqv&id=704866182938&clicktitle=%E4%B8%80%E7%94%9F%E5%BF%85%E5%90%AC%E7%9A%84%E7%94%B5%E5%BD%B1%E9%9F%B3%E4%B9%90%E2%80%94%E2%80%94%E3%80%8A%E5%8D%A1%E5%86%9C%E3%80%8B%E3%80%8A%E6%B5%B7%E4%B8%8A%E9%92%A2%E7%90%B4%E5%B8%88%E3%80%8B%E3%80%8A%E6%95%99%E7%88%B6%E3%80%8B%E3%80%8A%E6%B1%89%E5%B0%BC%E6%8B%94%E3%80%8B%E9%92%A2%E7%90%B4%E5%B0%8F%E6%8F%90%E7%90%B4%E5%A4%A7%E6%8F%90%E7%90%B4%E6%B5%AA%E6%BC%AB%E9%82%82%E9%80%85%E9%9F%B3%E4%B9%90%E4%BC%9A"
class Concert:
    def __init__(self):
        self.status = 0         # 状态,表示如今进行到何种程度
        self.login_method = 1   # {0:模拟登录,1:Cookie登录}自行选择登录方式
        self.driver = webdriver.Chrome(executable_path='chromedriver.exe')        # 默认Chrome浏览器
def set_cookie(self):
    self.driver.get(damai_url)
    print("###请点击登录###")
    while self.driver.title.find('大麦网-全球演出赛事官方购票平台') != -1:
        sleep(1)
    print('###请扫码登录###')

    while self.driver.title != '大麦网-全球演出赛事官方购票平台-100%正品、先付先抢、在线选座！':
       sleep(1)
    print("###扫码成功###")
    pickle.dump(self.driver.get_cookies(), open("cookies.pkl", "wb"))
    print("###Cookie保存成功###")
    self.driver.get(target_url)
def get_cookie(self):
    try:
        cookies = pickle.load(open("cookies.pkl", "rb"))  # 载入cookie
        for cookie in cookies:
            cookie_dict = {
                'domain':'.damai.cn',  # 必须有，不然就是假登录
                'name': cookie.get('name'),
                'value': cookie.get('value')
            }
            self.driver.add_cookie(cookie_dict)
        print('###载入Cookie###')
    except Exception as e:
        print(e)
    def login(self):
        if self.login_method==0:
            self.driver.get(login_url)
            # 载入登录界面
            print('###开始登录###')

        elif self.login_method==1:
            if not os.path.exists('cookies.pkl'):
            # 如果不存在cookie.pkl,就获取一下
                self.set_cookie()
            else:
                self.driver.get(target_url)
                self.get_cookie()
def enter_concert(self):
    """打开浏览器"""
    print('###打开浏览器，进入大麦网###')
    # self.driver.maximize_window()           # 最大化窗口
    # 调用登陆
    self.login()                            # 先登录再说
    self.driver.refresh()                   # 刷新页面
    self.status = 2                         # 登录成功标识
    print("###登录成功###")
    # 后续德云社可以讲
    if self.isElementExist('/html/body/div[2]/div[2]/div/div/div[3]/div[2]'):
        self.driver.find_element_by_xpath('/html/body/div[2]/div[2]/div/div/div[3]/div[2]').click()
def isElementExist(self, element):
    flag = True
    browser = self.driver
    try:
        browser.find_element_by_xpath(element)
        return flag

    except:
        flag = False
        return flag
def choose_ticket(self):
    if self.status == 2:                  #登录成功入口
        print("="*30)
        print("###开始进行日期及票价选择###")
        while self.driver.title.find('确认订单') == -1:           # 如果跳转到了订单结算界面就算这步成功了，否则继续执行此步
            try:
                buybutton = self.driver.find_element_by_class_name('buybtn').text
                if buybutton == "提交缺货登记":
                    # 改变现有状态
                    self.status=2
                    self.driver.get(target_url)
                    print('###抢票未开始，刷新等待开始###')
                    continue
                elif buybutton == "立即预定":
                    self.driver.find_element_by_class_name('buybtn').click()
                    # 改变现有状态
                    self.status = 3
                elif buybutton == "立即购买":
                    self.driver.find_element_by_class_name('buybtn').click()
                    # 改变现有状态
                    self.status = 4
                # 选座购买暂时无法完成自动化
                elif buybutton == "选座购买":
                    self.driver.find_element_by_class_name('buybtn').click()
                    self.status = 5
            except:
                print('###未跳转到订单结算界面###')
            title = self.driver.title
            if title == '选座购买':
                # 实现选座位购买的逻辑
                self.choice_seats()
            elif title == '确认订单':
                while True:
                    # 如果标题为确认订单
                    print('waiting ......')
                    if self.isElementExist('//*[@id="container"]/div/div[9]/button'):
                        self.check_order()
                        break
    def choice_seats(self):
        while self.driver.title == '选座购买':
            while self.isElementExist('//*[@id="app"]/div[2]/div[2]/div[1]/div[2]/img'):
                # 座位手动选择 选中座位之后//*[@id="app"]/div[2]/div[2]/div[1]/div[2]/img 就会消失
                print('请快速的选择您的座位！！！')
            # 消失之后就会出现 //*[@id="app"]/div[2]/div[2]/div[2]/div
            while self.isElementExist('//*[@id="app"]/div[2]/div[2]/div[2]/div'):
                # 找到之后进行点击确认选座
                self.driver.find_element_by_xpath('//*[@id="app"]/div[2]/div[2]/div[2]/button').click()
def check_order(self):
    if self.status in [3,4,5]:
        print('###开始确认订单###')
        try:
            # 默认选第一个购票人信息
            self.driver.find_element_by_xpath('//*[@id="container"]/div/div[2]/div[2]/div[1]/div/label').click()
        except Exception as e:
            print("###购票人信息选中失败，自行查看元素位置###")
            print(e)
        # 最后一步提交订单
        time.sleep(0.5)  # 太快会影响加载，导致按钮点击无效
        self.driver.find_element_by_xpath('//div[@class = "w1200"]//div[2]//div//div[9]//button[1]').click()
def finish(self):
    self.driver.quit()
if __name__ == '__main__':          # 开始模拟运行
    try:
        con = Concert()             # 具体如果填写请查看类中的初始化函数
        con.enter_concert()         # 打开浏览器
        con.choose_ticket()         # 开始抢票

    except Exception as e:
        print(e)
        con.finish()
# python based
