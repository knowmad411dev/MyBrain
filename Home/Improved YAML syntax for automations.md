---
tags:
- automation
- home
---

# Improved YAML Syntax for Automations

With recent Home Assistant updates, the **YAML syntax for automations** has been improved to make it more intuitive. YAML (Yet Another Markup Language) is the file format Home Assistant uses to store automations. These changes aim to make the code easier to understand and work with.

But is the new syntax truly simpler? In this guide, we take a deep dive into these changes, compare them with the old style, and help you get comfortable with writing and updating automations.

---

## Section 1: Why Change the YAML Syntax?

First things first: **don’t panic!** The new YAML syntax is an improvement, but it won’t break any of your existing automations. You can continue using the old syntax if your current setup works well—Home Assistant has promised that the old syntax will remain compatible.

However, for new automations, Home Assistant recommends using the new syntax, especially if you use the Graphical Automation Editor, as it will automatically generate YAML using the new format. The new syntax is designed to be more natural, readable, and future-proof.

---

## Key Components of Automations

Before diving into the syntax changes, let's break down the **key components** of an automation:

- **Triggers** (required): What starts the automation (e.g., time, sensor changes, or a person arriving home). You can have multiple triggers.
- **Conditions** (optional): Rules that need to be true for the automation to run. By default, all conditions must be true, but logical operators like "or" can be used to change this.
- **Actions** (required): Tasks that are performed when the automation is triggered. Multiple actions can run in sequence, such as turning on lights or sending notifications.

---

## Section 2: What Has Changed in the YAML Syntax?

The new YAML syntax introduces a few key updates to make it more intuitive and reflective of how automations work:

1. **Plural Keys**

    - `trigger` → `triggers`
    - `condition` → `conditions`
    - `action` → `actions`

    Using plural forms makes it clear that multiple triggers, conditions, or actions can be included. This is more descriptive and represents the flexible nature of automations.

2. **Simplified Trigger Definition**
    Previously, the `platform` key specified trigger types (e.g., `platform: sun`), which made the code cumbersome. The new syntax simply uses the keyword `trigger`, making it cleaner and more readable.

---

## Section 3: What Does This Mean for You?

The new YAML syntax provides more flexibility, allowing you to easily define:

- **Multiple Triggers**: For example, based on time, motion detection, or someone's location.
- **Multiple Conditions**: Rules that all need to be true for the automation to execute (e.g., time window or occupancy).
- **Multiple Actions**: Actions to be performed sequentially, such as turning on lights and adjusting the thermostat.

---

## Example: New YAML Syntax

Here’s an example of an automation using the **new YAML syntax**. This automation turns on your lights one hour before sunset if someone is home and also turns on the lights if someone arrives home between 4 PM and 11 PM.

yaml

Copy code

`automation my_lights:   # Turns on lights 1 hour before sunset if people are home   # and if people get home between 16:00-23:00   - alias: "Rule 1: Light on in the evening"     triggers:       # Trigger configurations are prefixed with '-'       - trigger: sun         event: sunset         offset: "-01:00:00"  # 1 hour before sunset       - trigger: state         entity_id: all         to: "home"  # When someone arrives home     conditions:       # Condition configurations are prefixed with '-'       - condition: state         entity_id: all         state: "home"  # Only if someone is home       - condition: time         after: "16:00:00"  # Between 4 PM         before: "23:00:00"  # And 11 PM     actions:       # Single action entry can be prefixed with '-'       - action: homeassistant.turn_on         target:           entity_id: group.living_room  # Turns on the living room lights`

---

## Comparison to Old YAML Syntax

In the **old YAML syntax**, here’s how the automation would have looked:

yaml

Copy code

`automation:   - alias: "Rule 1: Light on in the evening"     trigger:       - platform: sun         event: sunset         offset: "-01:00:00"       - platform: state         entity_id: all         to: "home"     condition:       - condition: state         entity_id: all         state: "home"       - condition: time         after: "16:00:00"         before: "23:00:00"     action:       - action: homeassistant.turn_on         entity_id: group.living_room`

### Differences Explained:

1. **Triggers**:

    - Old syntax used `trigger` with `platform` keys.
    - New syntax uses `triggers` directly with types like `sun` or `state`.
2. **Conditions**:

    - Old syntax used the singular key `condition`.
    - New syntax uses `conditions` to clarify that multiple rules can be added.
3. **Actions**:

    - The key `action` has been replaced with `actions`.

---

## Editing YAML Automations in Home Assistant

Home Assistant provides a graphical interface to create automations, but they are all saved in **YAML format**. To fine-tune your automations:

1. Open **Home Assistant**.
2. Navigate to **Settings > Automations & Scenes**.
3. Select the automation to edit.
4. Click the menu (three dots) in the top-right corner and choose **Edit in YAML**.

This allows you to see and directly edit the YAML code.

---

## Conclusion

The new YAML syntax in Home Assistant is designed to make automations **clearer**, **more intuitive**, and **easier to work with**. The use of plural keys—like `triggers`, `conditions`, and `actions`—helps to clearly communicate that multiple entries are allowed.

While the old syntax will continue to work, it's recommended to learn and use the new format, especially for future automations. With practice, you'll find that writing, editing, and managing complex automations becomes much simpler.

---

## Quiz

Test your understanding of the new YAML syntax:

1. **What is the main reason for updating the YAML syntax for automations?**

    - B) To make the code more intuitive and easier to read
2. **Which of the following is correct in the new YAML syntax?**

    - C) `trigger`
3. **True or False: The old YAML syntax for automations will stop working after the update.**

    - False
4. **What is the new term used to define multiple steps that trigger an automation?**

    - D) `triggers`
5. **How do you define multiple conditions in the new YAML syntax?**

    - A) Using the key `conditions`
6. **Which part of the following automation is incorrect based on the new syntax?**

    - D) Both A and B (Use `triggers` and `conditions` instead of `trigger` and `condition`)
7. **Which key lists tasks that happen after the automation is triggered?**

    - C) `actions`
8. **How do you specify a sunset trigger in the new YAML syntax?**

    - A) `trigger: sun`
9. **Which section can contain optional conditions before performing actions?**

    - B) `conditions`

---

### How Did You Do?

- **8-9 correct**: YAML master!
- **6-7 correct**: Well done!
- **4-5 correct**: Good effort!
- **3 or below**: Review the material and try again!

---

### Related Topics

[[Home]] [[Obsidian YAML]]
