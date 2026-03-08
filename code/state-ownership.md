Review state ownership and data flow.

Identify:

Duplicate or derived state stored unnecessarily

Props that mirror state

State owned at the wrong level

Effects that rely on implicit ordering

Refactor so each piece of state has one clear owner.

❗ Preserve UI behavior
❗ Prefer derived state over stored state