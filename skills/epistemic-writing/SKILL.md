---
name: epistemic-writing
description: Writing in clear and concise language to present reasoned thinking and genuine, concrete emotions.
---

# Epistemic Writing

## When to use

- When you need to produce a piece of writing on a specific topic.

## Goal

- Presenting reasoned thinking and genuine, concrete emotions in clear and concise language.
- The output should contain two KEY ELEMENTS, it will fail if lack of either one of them:
  - Opinions/Thoughts/Ideas/Arguments/Conclusions
  - Evidence/Examples/Data/Details/References

## SOP

1. Create an outline to organize the KEY ELEMENTS, follow the standard defined in [three-level-note-taking](../three-level-note-taking/SKILL.md).
2. Write the content based on the outline.
3. Review the content
    1. If the outline can be improved, go back to step 1.
    2. If the content can be improved, go back to step 2.
4. Finalize the content if the content is good enough.

### Note

- **Ask for additional input if you think the input is not enough to produce a good output.**

### Structure of the output

- It should be an standard markdown text. Put the outline in the metadata of the markdown text, and the content in the body of the markdown text.

## Example

### Input

写一篇短文，说明为什么我不再把熬夜工作当成努力。背景：我连续三周凌晨一点以后睡；其间有 12 次提交发生在晚上十一点以后，其中 3 次第二天被我自己回滚；一次周末午饭时，朋友重复问了我两遍问题，我还是没听进去，我因此感到羞愧。现在我每天十点半停止工作，写下明天最重要的三件事。实行两周后，没有再回滚提交，白天也更能集中注意力。

### Output

````markdown
---
outline: |
  - L1 熬夜制造了努力的感觉，却降低了工作的可靠性
    - L2 深夜产出并不等于有效产出
      - L3 三周内有 12 次深夜提交，其中 3 次第二天被回滚
    - L2 疲惫还侵占了工作之外的生活
      - L3 午饭时没听见朋友重复两遍的问题，因此感到羞愧
  - L1 给工作设置终点，反而让努力更持续
    - L2 每晚十点半停工，并写下次日最重要的三件事
      - L3 两周内没有再回滚提交，白天的注意力也更集中
---

# 我不再把深夜在线当成努力

过去，我把凌晨还亮着的屏幕当成一种证明：只要我比别人睡得晚，就说明我更认真。现在我不再相信这个判断。努力不能只看投入了多少时间，还要看这些时间是否带来了可靠的结果。

让我改变想法的是一组不太体面的记录。连续三周，我都在凌晨一点以后睡。那段时间共有 12 次提交发生在晚上十一点以后，其中 3 次在第二天被我自己回滚。深夜里的我觉得问题已经解决；睡醒后再看，才发现有的改动遗漏了边界条件，有的只是把复杂性挪到了别处。那些提交不是额外的进展，而是透支第二天来制造当晚的成就感。

疲惫也越过了工作的边界。一次周末午饭，朋友把同一个问题问了两遍，我仍然没有听进去。看到他停下来等我时，我感到羞愧。那一刻我意识到，我所谓的勤奋正在让身边的人面对一个心不在焉的我。这不是我愿意用工作换来的生活。

后来，我给每天的工作设了一个简单的终点：晚上十点半停下来，只写下第二天最重要的三件事。最初关掉电脑时，我仍会焦虑，像是提前离开了一场只有我知道的比赛。但实行两周后，我没有再回滚过提交，白天也更容易把一个问题从头想到尾。

我并不是从此拒绝所有加班。真正紧急的事情仍然值得多投入时间。但我不再把熬夜本身视为美德。对我而言，更可信的努力，是今天清醒地完成重要的事，也给明天留下一个能继续思考的人。
````
