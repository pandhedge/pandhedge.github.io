---
layout: post
title:  "基于python生成树状图"
date:   2025-08-28 03:38:00 +0800
categories: python
tags: python project treemap 
author: PandHedge
mathjax: true
---

* content
{:toc}


## 概述



  以下基于python 生成自定义树状图，有基于treelib和不借助其他库的两种方法。

---

## 项目详情



```python
def generate_custom_tree(nodes, parent_id=None, indent=""):
    """
    生成自定义文字树形图
    :param nodes: 节点列表，每个节点含 id, parent_id, text（自定义文字）
    :param parent_id: 父节点ID（用于递归）
    :param indent: 缩进（控制层级显示）
    :return: 树形文本字符串
    """
    tree_text = ""
    # 筛选当前父节点的子节点
    children = [node for node in nodes if node["parent_id"] == parent_id]
    
    for i, child in enumerate(children):
        # 控制末尾节点的符号（最后一个子节点用 "└─"，其余用 "├─"）
        prefix = "└─ " if i == len(children) - 1 else "├─ "
        # 添加当前节点的自定义文字
        tree_text += f"{indent}{prefix}{child['text']}\n"
        
        # 递归处理子节点（增加缩进，区分层级）
        child_indent = indent + ("   " if i == len(children) - 1 else "│  ")
        tree_text += generate_custom_tree(nodes, child["id"], child_indent)
    
    return tree_text

# --------------------------
# 1. 自定义节点数据（文字可任意改）
custom_nodes = [
    {"id": 1, "parent_id": None, "text": "🏢 总公司"},  # 根节点（parent_id=None）
    {"id": 2, "parent_id": 1, "text": "👥 人力资源部"},   # 一级节点
    {"id": 3, "parent_id": 1, "text": "💻 技术研发中心"}, # 一级节点
    {"id": 4, "parent_id": 2, "text": "招聘组"},          # 二级节点
    {"id": 5, "parent_id": 2, "text": "薪酬绩效组"},    # 二级节点
    {"id": 6, "parent_id": 3, "text": "后端开发组"},      # 二级节点
    {"id": 7, "parent_id": 6, "text": "Java团队"}         # 三级节点
]

# 2. 生成并打印树形图
tree_result = generate_custom_tree(custom_nodes)
print(tree_result)
```



```python
from treelib import Tree
from treelib.exceptions import DuplicatedNodeIdError

def create_filesystem_tree():
    # 创建树实例（根节点为“根目录”）
    tree = Tree()
    tree.create_node("Root Directory", "root")  # (节点名称, 唯一ID)
    
    # 一级目录：Documents/Pictures/Music/Programs
    tree.create_node("Documents", "docs", parent="root")
    tree.create_node("Pictures", "pics", parent="root")
    tree.create_node("Music", "music", parent="root")
    tree.create_node("Programs", "prog", parent="root")
    
    # Documents 下的内容
    tree.create_node("Notes.txt", "notes", parent="docs")
    tree.create_node("Report.pdf", "report", parent="docs")
    tree.create_node("Projects", "projects", parent="docs")
    
    # Projects 下的内容（三级节点）
    tree.create_node("Python", "python", parent="projects")
    tree.create_node("Java", "java", parent="projects")
    tree.create_node("C++", "cpp", parent="projects")
    
    # Pictures 下的内容
    tree.create_node("Family.jpg", "family", parent="pics")
    tree.create_node("Nature", "nature", parent="pics")
    tree.create_node("Vacation", "vacation", parent="pics")
    
    # Music 下的内容
    tree.create_node("Rock", "rock", parent="music")
    tree.create_node("Jazz", "jazz", parent="music")
    
    # Programs 下的内容
    tree.create_node("Browser.exe", "browser", parent="prog")
    tree.create_node("Editor.app", "editor", parent="prog")
    
    return tree

def display_fixed_tree(tree):
    """修复后的自定义树显示：层级对齐、线条完整"""
    if not tree:
        return
    print("Fixed File System Structure:")
    print("=============================")
    
    # 存储“父节点是否为最后一个子节点”的状态（用于绘制竖线）
    # 例如：[False, True] 表示“一级父节点不是最后一个，二级父节点是最后一个”
    parent_is_last = []
    
    def print_node(node_id):
        # 获取当前节点的深度和父节点
        depth = tree.depth(node_id)
        node = tree[node_id]
        parent_node = tree.parent(node_id)
        
        # 1. 处理缩进和竖线（关键：根据父节点状态判断是否显示竖线）
        indent = ""
        if depth > 0:
            # 遍历所有父节点的“是否最后一个”状态
            for is_last in parent_is_last[:-1]:  # 排除当前父节点（最后一个元素）
                # 非最后一个父节点：显示竖线（保持层级连贯）；最后一个：显示空格
                indent += "│   " if not is_last else "    "
            # 处理当前父节点的连接线（└── 或 ├──）
            current_parent_is_last = parent_is_last[-1] if parent_is_last else False
            indent += "└── " if current_parent_is_last else "├── "
        
        # 2. 打印当前节点
        print(f"{indent}{node.tag}")
        
        # 3. 递归打印子节点（先获取所有子节点，保持顺序）
        children = tree.children(node_id)
        if children:
            for i, child in enumerate(children):
                # 记录当前子节点是否为“父节点的最后一个子节点”
                is_last_child = (i == len(children) - 1)
                parent_is_last.append(is_last_child)
                # 递归打印子节点
                print_node(child.identifier)
                # 回溯：删除当前子节点的状态（避免影响其他分支）
                parent_is_last.pop()
    
    # 从根节点开始递归打印
    print_node("root")

if __name__ == "__main__":
    # 1. 创建文件树
    fs_tree = create_filesystem_tree()
    
    # 2. 显示库自带的正确结果（作为对比）
    print("=== Library Default Display (Correct) ===")
    fs_tree.show()
    print("\n" + "="*60 + "\n")
    
    # 3. 显示修复后的自定义结果（解决“线断”问题）
    display_fixed_tree(fs_tree)
    
    # 4. 保存修复后的结果到文件
    with open("fixed_filesystem_tree.txt", "w", encoding="utf-8") as f:
        # 重定义打印函数，将内容写入文件（而非控制台）
        parent_is_last = []
        def write_node(node_id):
            depth = fs_tree.depth(node_id)
            node = fs_tree[node_id]
            parent_node = fs_tree.parent(node_id)
            indent = ""
            if depth > 0:
                for is_last in parent_is_last[:-1]:
                    indent += "│   " if not is_last else "    "
                current_parent_is_last = parent_is_last[-1]
                indent += "└── " if current_parent_is_last else "├── "
            f.write(f"{indent}{node.tag}\n")
            children = fs_tree.children(node_id)
            for i, child in enumerate(children):
                is_last_child = (i == len(children) - 1)
                parent_is_last.append(is_last_child)
                write_node(child.identifier)
                parent_is_last.pop()
        write_node("root")
    print("\nFixed tree saved to 'fixed_filesystem_tree.txt'")
```



---

## 总结
