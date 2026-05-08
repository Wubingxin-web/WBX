# 校园空间调度智能助手 - 主程序
# 基于 AI Agent + 多任务调度 + 规则知识库

def show_welcome():
    print("=" * 50)
    print("    校园空间调度智能助手")
    print("    Campus Space Scheduling Assistant")
    print("=" * 50)
    print("功能：场地查询 | 预约申请 | 冲突检测 | 规则咨询")
    print("输入 help 查看帮助\n")

def show_help():
    print("\n【使用说明】")
    print("1. 查询：输入 查询报告厅 / 查询实验室 / 查询体育馆")
    print("2. 预约：输入 预约+场地+时间")
    print("3. 规则：输入 规则")
    print("4. 退出：输入 exit\n")

# 模拟场地信息
venues = {
    "报告厅": {"可用时段": ["09:00-11:00", "14:00-16:00"], "容量": 200},
    "实验室": {"可用时段": ["10:00-12:00", "15:00-17:00"], "容量": 40},
    "体育馆": {"可用时段": ["08:00-22:00"], "容量": 500}
}

# 校园规则
rules = """
【校园场地使用规则】
1. 报告厅需提前3天预约
2. 实验室仅限教学使用
3. 体育馆单次预约不超过4小时
4. 迟到30分钟自动取消预约
"""

def query_venue(name):
    if name in venues:
        info = venues[name]
        return f"\n【{name}信息】\n容量：{info['容量']}人\n可用时段：{info['可用时段']}"
    else:
        return "\n暂无该场地信息"

def book_venue(name, time):
    if name not in venues:
        return "预约失败：场地不存在"
    if time in venues[name]["可用时段"]:
        return f"✅ 预约成功！已预约 {name} {time}"
    else:
        return f"❌ 预约失败：该时段不可用"

def main():
    show_welcome()
    while True:
        user = input("请输入指令：")
        if user == "exit":
            print("谢谢使用！")
            break
        elif user == "help":
            show_help()
        elif user == "规则":
            print(rules)
        elif "查询" in user:
            if "报告厅" in user:
                print(query_venue("报告厅"))
            elif "实验室" in user:
                print(query_venue("实验室"))
            elif "体育馆" in user:
                print(query_venue("体育馆"))
            else:
                print("请输入正确场地名称")
        elif "预约" in user:
            if "报告厅" in user:
                print(book_venue("报告厅", "09:00-11:00"))
            elif "实验室" in user:
                print(book_venue("实验室", "10:00-12:00"))
            elif "体育馆" in user:
                print(book_venue("体育馆", "08:00-22:00"))
            else:
                print("预约格式：预约 场地 时间")
        else:
            print("输入 help 查看使用方法")

if __name__ == "__main__":
    main()
