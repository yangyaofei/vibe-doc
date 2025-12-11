# 交接与上下文协议 (Handover Protocol)

## 1. 读取规则 (Start)
* 每次对话开始时，**必须**检查 `docs/handovers/` 目录下序号最大的文件 (如 `005_xxx.md`)。
* 这是你唯一的“短期记忆”恢复点。

## 2. 写入规则 (End)
* 在达到对话上限、任务完成或中止时，**必须**生成新的交接文件。
* **命名**: `docs/handovers/{NNN+1}_{description}.md`
* **内容模板**:
    ```markdown
    # Handover Document
    ## 1. Status (当前状态)
    * 总体进度: ...
    * 阻塞点: ...
    
    ## 2. History (本次会话产出)
    * 完成了 Step X, Y...
    * 修改了文件 A, B...
    
    ## 3. Next Steps (下一步计划)
    * 具体要做的指令列表...
    
    ## 4. Execution Guide (避坑指南)
    * 对下一个 Agent 的特别叮嘱 (Technical limitations, potential bugs)...
    ```