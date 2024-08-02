# 暑期資料結構期中報告-學號:11024236 學生:黃言哲


## 期中題目五: Python之雙鍊錶

### 雙鍊錶簡述
結構鍊錶（雙向鍊錶）是一種鍊式資料結構，它的每個節點都包含兩個指針，一個指向前一個節點，一個指向後一個節點。進行插入和刪除操作，因為每個節點都可以透過前向或後向指標存取其前驅和後繼。

![01](https://github.com/Dopo2002/report/blob/main/pic2.png)
## 圖例說明
![01](https://github.com/Dopo2002/report/blob/main/pic1.png)
## 代碼作用
Node 類：

__init__(self, item): 初始化一個節點，包含值 item 以及前後指針 next 和 prior。

FunctionLink 類：
__init__(self): 初始化鏈表，包含鏈表長度 linklength 和頭節點 head。

creatLinkListHead(self, li): 以頭插法創建鏈表。遍歷輸入的列表，創建新節點並插入到鏈表頭部。

creatLinkListTail(self, li): 以尾插法創建鏈表。遍歷輸入的列表，創建新節點並插入到鏈表尾部。

printLinkList(self, lk): 打印鏈表中的所有節點值。

inserLinkList(self, index, element, curNode): 在鏈表的指定位置插入一個新節點。

deleteLinkList(self, index, curNode): 刪除鏈表中指定位置的節點。
## 具體代碼
    class Node(object):
    """
    定義雙向鏈表的節點
    """
    def __init__(self, item):
        self.item = item  # 節點的值
        self.next = None  # 指向下一個節點的指針
        self.prior = None  # 指向前一個節點的指針


    class FunctionLink(object):
    """
    定義雙向鏈表的各種操作
    """
    def __init__(self):
        self.linklength = 1  # 鏈表的長度
        self.head = None  # 初始化，頭節點指向空

    def creatLinkListHead(self, li):
        """
        以頭插法創建鏈表
        :param li: 傳入一個列表
        :return: 返回鏈表的頭節點
        """
        head = Node(li[0])
        for element in li[1:]:
            self.linklength += 1
            node = Node(element)  # 創建一個新節點
            node.next = head  # 新節點指向當前的頭節點
            head.prior = node  # 當前頭節點的前指針指向新節點
            head = node  # 更新頭節點
        return head

    def creatLinkListTail(self, li):
        """
        以尾插法創建鏈表
        :param li: 傳入一個列表
        :return: 返回鏈表的頭節點
        """
        head = Node(li[0])
        current = head
        for element in li[1:]:
            self.linklength += 1
            node = Node(element)  # 創建一個新節點
            current.next = node  # 當前節點的下一個指針指向新節點
            node.prior = current  # 新節點的前指針指向當前節點
            current = node  # 更新當前節點
        return head

    def printLinkList(self, lk):
        """
        打印鏈表中的所有節點值
        :param lk: 傳入頭節點
        :return: 無返回值
        """
        while lk:
            if not lk.next:
                print(lk.item)
            else:
                print(lk.item, end=", ")
            lk = lk.next

    def inserLinkList(self, index, element, curNode):
        """
        在鏈表的指定位置插入一個新節點
        :param index: 要插入的位置索引
        :param element: 新節點的值
        :param curNode: 頭節點
        :return: 無返回值
        """
        head = curNode  # 保存頭節點
        number = 1
        if index > self.linklength:
            raise Exception("對不起您輸入的索引值超過了鏈表的長度")
        else:
            while True:
                if index == number:
                    p = Node(element)  # 創建新節點
                    p.next = curNode.next  # 新節點的下一個指針指向當前節點的下一個節點
                    curNode.next.prior = p  # 當前節點的下一個節點的前指針指向新節點
                    p.prior = curNode  # 新節點的前指針指向當前節點
                    curNode.next = p  # 當前節點的下一個指針指向新節點
                    self.linklength += 1
                    curNode = head  # 恢復頭節點
                    break
                else:
                    curNode = curNode.next
                    number += 1

    def deleteLinkList(self, index, curNode):
        """
        刪除鏈表中指定位置的節點
        :param index: 要刪除的索引位置
        :param curNode: 頭節點
        :return: 無返回值
        """
        head = curNode  # 保存頭節點
        number = 1
        if index > self.linklength:
            raise Exception("對不起，您輸入的索引位置超過了鏈表的長度，請重新輸入")
        else:
            while True:
                if number == index:
                    p = curNode.next  # 暫存待刪除節點
                    curNode.next = p.next  # 當前節點的下一個指針指向待刪除節點的下一個節點
                    if p.next:
                        p.next.prior = curNode  # 待刪除節點的下一個節點的前指針指向當前節點
                    self.linklength -= 1
                    curNode = head  # 恢復頭節點
                    break
                else:
                    curNode = curNode.next
                    number += 1


          if __name__ == '__main__':
            func = FunctionLink()
            doublelk = func.creatLinkListHead([1, 2, 3, 4])
            func.printLinkList(doublelk)
            func.inserLinkList(2, 10, doublelk)
            func.printLinkList(doublelk)
            func.deleteLinkList(2, doublelk)
            func.printLinkList(doublelk)

## 運行結果
![01](https://github.com/Dopo2002/report/blob/main/code.jpg)
