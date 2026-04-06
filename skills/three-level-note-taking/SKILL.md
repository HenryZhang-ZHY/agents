---
name: three-level-note-taking
description: Distilling information into three levels of notes. Use when taking notes on a given text.
---

# Three-Level Note-Taking

## Goal

- Understanding the conclusions and arguments
- Collecting materials for future uses

## Concepts

- Level 1 items are the key concepts to define the problem and explain the the problem.
- Level 2 items are the definitions and details that support the level 1 items.
- Level 3 items are the examples、evidence、data and references that support the level 2 items.

## How to do it

- Input: a text to take notes on
- Output: a multi-level unordered markdown list to organize the notes as a tree structure.

1. Find keywords and phrases in the text.
2. Organize the keywords and phrases into level 1 and level 2 items.
3. Find level 3 items that support the level 2 items.
4. Create a multi-level unordered markdown list to organize the notes as a tree structure.

### Rules

- There can be 1..n level 1 items
- Each level 1 item can have 1..n level 2 items
- Each level 2 item can have 0..n level 2 items or 1..n level 3 items
- Since there could be nested items in the same level, add marks L1, L2, L3 at the beginning of each item to indicate the level of the item.

## Examples

### Example 1

#### Input

我的新生活观
蔡元培

什么叫旧生活？是枯燥的，是退化的。什么叫新生活？是丰富的，是进步的。

旧生活的人，是一部分不做工，又不求学的，终日把吃着嫖赌做消遣。物质上一点也没生产，精神上也一点没长进。有一部分是整体做苦工，没有机会求学。身体上疲乏得了不得，所做的工是事倍功半，精神上得过且过。岂不全是枯燥的吗？不做工的人，体力是逐渐衰退了；不求学的人，心力又逐渐萎靡了。一代传一代，更衰退，更萎靡。岂不全是退化吗？新生活的每一个人，每日有一定所做工，又有一定的时候求学。所以制品日日增加。这不是丰富的吗？工是愈练愈熟的，熟了出产必能加多，而且熟能生巧，就能增出新工作来。学是有一部分讲现在做工的道理，懂了这个道理，工作必能改良。又有一部分讲别种工作的道理，懂了那种道理又可以改良别种的工。

从简单的工改到复杂的工，从容易的工改到繁难的工，从出产较少的工改到出产较多的工。而且有一种学问虽然与工作没有直接的关系，但是学了以后，眼光一日一日的远大起来，心地一日一日的平和起来，生活上无形中增进许多幸福。这还不是进步吗？

要是有一个人肯日日做工，日日求学，便是一个新生活的人；有一个团体里面的人，都是日日做工，日日求学，便是一个新生活的团体；全世界的人都是日日做工，日日求学，那就是新生活的世界了。

#### Output
- L1 《我的新生活观》 蔡元培
  - L2 旧生活：退步的生活
    - L2 一部分人：不做工又不求学，终日把吃着嫖赌做消遣
      - L3 物质上没有生产，精神上也没有长进
      - L3 不做工，体力衰退
    - L2 穷人： 整体做苦工，没有机会求学
      - L3 身体上疲乏得不得了
        - L3 不求学，心理逐渐萎靡
      - L3 所做的事是事倍功半
        - L3 因为没知识
    - L2 两种人：一代传一代，更衰退，更萎靡，全是退化
  - L2 新生活：进步的生活
    - L2 平等的社会
    - L2 每个人每日有一定所做工，又有一定的时候求学
      - L3 丰富
        - L3 因为人人工作，所以制品日日增加，而不是由一部分工作的人养活另一部分不工作的人
        - L3 因为每日工作，熟练度更高，增加了产出
        - L3 因为每日学习，生产复杂度提升，新的工作岗位不断产生
      - L3 知识如何带来生产的丰富和进步
        - L3 学习专业知识 —— 工作得到改良
        - L3 学习其他专业知识 —— 有能力改良各种专业技能
        - L3 一个人可以自由选择想从事的专业，因为学习的、进步的人，有能力学会各种专业
      - L3 知识如何带来生活的丰富和幸福
        - L3 学习非专业知识，看似和工作无关的学习，但是眼界一日一日的远大起来，心地一日一日的平和起来，生活上无形中增进许多幸福
  - L2 推导出命题： 从个人到社会，到整个人类，都应该追求每日做工，每日学习的丰富，进步的生活
    - L3 要是有一个人肯日日做工，日日求学，便是一个新生活的人
    - L3 有一个团体里面的人，都是日日做工，日日求学，便是一个新生活的团体
    - L3 全世界的人都是日日做工，日日求学，那就是新生活的世界了
