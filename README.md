# agent-speak-readability

> An agent skill that makes an agent's natural-language output readable to a
> human reader. Cross-language rules live in `SKILL.md`. Chinese rules live in
> `lang/zh/`. English rules live in `lang/en/`. The core of the skill is a
> pre-send check written as edit steps, not as a quality to aim at.

本仓库是一个技能（skill）。
这一个技能让智能体写给人看的自然语言变得可读。

## 这一个技能解决什么问题

智能体写字的时候，智能体是在写给自己看。
智能体已经知道执行者、对象、文件名和结果，所以智能体把上述成分压缩掉了。
读这一段话的人并不知道上述成分。
于是智能体写出的这一段话看上去很有把握，实际上几乎不携带信息。

本仓库不是一份文风偏好。
本仓库是一串我在发送之前必须做完的编辑动作。

## 目录结构

```
agent-speak-readability/
├── README.md                      本文件
├── SKILL.md                       技能入口：九条通用原则 + 发送前检查
├── AGENTS.md                      本仓库的全局约束（从全局 CLAUDE.md 拷贝并删减）
├── CLAUDE.md                      指向 AGENTS.md 的符号链接
├── docs/
│   └── suggested-claude-md-section.md   给用户全局 CLAUDE.md 的替换建议
└── lang/
    ├── zh/
    │   ├── PRINCIPLES.md          中文附加原则 Z1 到 Z10
    │   ├── ACCEPTANCE-CASES.md    用户亲手写的四条修改意见（逐字保留）
    │   └── NEGATIVE-SAMPLES.md    真实会话里的中文反面样本
    └── en/
        └── PRINCIPLES.md          英文附加原则 E1 到 E9
```

## 使用者怎么用

1. 智能体读 `SKILL.md`，智能体拿到九条通用原则。
2. 智能体按当前书写的语言读 `lang/zh/` 或者 `lang/en/`。
3. 智能体写完草稿以后，智能体执行 `SKILL.md` 第 4 节的十个检查步骤。
4. 智能体再执行语言文件末尾的附加检查步骤。
5. 智能体发出改好的文字。

用户说「看不懂」的时候，智能体重新执行上述检查步骤，智能体直接发出改写后的文字。

## 安装命令（请用户自己执行）

本仓库没有自动安装自己。
用户想安装本仓库的时候，用户自己执行下面这一条命令。

```bash
ln -s /Users/zzn/ws/xinbenlv/agent-speak-readability ~/.claude/skills/agent-speak-readability
```

用户还可以读 `docs/suggested-claude-md-section.md`。
上述文件给出了全局 `~/.claude/CLAUDE.md` 里「与用户交流的语言的原则」一节的替换建议。
我没有改动用户的全局文件，原因是用户自己的规则要求我先取得明确的手动批准。

## 开发者怎么改

`lang/zh/ACCEPTANCE-CASES.md` 里的第一个代码块是验收标准。
开发者改动本仓库以后，开发者先拿改动后的内容对照上述四条修改意见检查一遍。
上述代码块里的字逐字保留，开发者不要改写。

开发者写进本仓库的每一句话也必须通过本仓库自己的检查步骤。
写一份可读性技能却写出不可读的句子，这件事本身就自相矛盾。

## 这一个技能从哪里来

一位中文母语的用户在一次长会话里读不懂智能体写的中文。
这位用户的全局配置文件里已经有了十三条写作规则。
智能体读完了上述配置文件。用户又在提示词里重申了一遍要求。智能体在紧接着的一条回复里仍然违反了七次。
同一个配置文件里的动作约束（例如「没有用户要求就不许提交」）却保持了好几个小时。
所以本仓库把要求写成了「发送之前做完这几个动作」，本仓库没有把要求写成「写得清楚一点」。
