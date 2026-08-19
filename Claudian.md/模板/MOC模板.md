---
type: moc
target-tag:
---

# {{title}} · MOC

## 相关卡片（自动聚合）
```dataview
LIST
FROM "笔记/卡片/原子卡片"
WHERE contains(file.tags, this.target-tag)
SORT created DESC
```
