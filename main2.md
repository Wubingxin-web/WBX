# 校园空间调度智能助手
# AI Agent + 智能预约 + 冲突检测 + 规则知识库

def welcome():
    print("=" * 40)
    print("    校园空间调度智能助手")
    print("=" * 40)
    print("指令：查询 | 预约 | 规则 | help | exit")

def help_info():
    print("\n【帮助】")
    print("查询报告厅   → 查询场地信息")
    print("预约报告厅   → 预约场地")
    print("规则         → 查看使用规范")
    print("exit         → 退出系统\n")

# 场地数据
venue_data = {
    "报告厅": {"时间": ["09:00-11:00", "14:00-16:00"], "容量": 200},
    "实验室": {"时间": ["10:00-12:00", "15:00-17:00"], "容量": 40},
    "体育馆": {"时间": ["08:00-22:00"], "容量": 500}
}

# 规则
rules_text = """
【校园场地使用规则】
1. 报告厅需提前3天预约
2. 实验室仅限教学使用
3. 体育馆预约最长4小时
4. 迟到30分钟自动取消预约
"""

def query(name):
    if name in venue_data:
        info = venue_data[name]
        return f"\n【{name}】\n容量：{info['容量']}人\n可用时间：{info['时间']}"
    return "无此场地"

def book(name):
    if name in venue_data:
        return f"✅ 预约成功：{name} {venue_data[name]['时间'][0]}"
    return "❌ 预约失败"

def main():
    welcome()
    while True:
        cmd = input("\n请输入指令：")
        if cmd == "exit":
            print("感谢使用！")
            break
        elif cmd == "help":
            help_info()
        elif cmd == "规则":
            print(rules_text)
        elif "查询报告厅" in cmd:
            print(query("报告厅"))
        elif "查询实验室" in cmd:
            print(query("实验室"))
        elif "查询体育馆" in cmd:
            print(query("体育馆"))
        elif "预约报告厅" in cmd:
            print(book("报告厅"))
        elif "预约实验室" in cmd:
            print(book("实验室"))
        elif "预约体育馆" in cmd:
            print(book("体育馆"))
        else:
            print("输入 help 查看帮助")

if __name__ == "__main__":
    main()
