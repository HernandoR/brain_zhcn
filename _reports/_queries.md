---
fleeting_monthly: |
  TABLE
    "https://brain.d.foundation/%CE%A9+Fleeting+notes/" + rows.file.name as entries,
    rows.file.tags as tags,
    sum(rows.icy) + " ICY" as reward
  FROM "Ω Fleeting notes"
  WHERE discord_id != NULL
    AND date.weekyear >= (date(today)).weekyear - 3
  GROUP BY discord_id

structured_permanent_notes_monthly: |
  TABLE
    rows.file.link as entries, 
    rows.file.tags as tags
  FROM #engineering OR #writing OR #design OR #communication OR #blockchain
  WHERE author != NULL
    AND date.weekyear >= (date(today)).weekyear - 3
  GROUP BY author

literature_notes_monthly: |
  TABLE
    "https://brain.d.foundation/%CE%A9+Literature+notes/" + rows.file.name as entries,
    rows.file.tags as tags,
    sum(rows.icy) + " ICY" as reward
  FROM "Ω Literature notes"
  WHERE discord_id != NULL
    AND date.weekyear >= (date(today)).weekyear - 3
  GROUP BY discord_id

permanent_notes_monthly: |
  TABLE
    "https://brain.d.foundation/%CE%A9+Permanent+notes/" + rows.file.name as entries,
    sum(rows.icy) + " ICY" as reward
  FROM "Ω Permanent notes"
  WHERE discord_id != NULL
    AND date.weekyear >= (date(today)).weekyear - 3
  GROUP BY discord_id

fleeting_notes_all: |
  TABLE discord_id, discord_channel, date, "#" + regexreplace(tags, ", ", " #") as tags, icy
  FROM "Ω Fleeting notes"
  WHERE discord_id != NULL

structured_permanent_notes_all: |
  TABLE
    author,
    date,
    "#" + regexreplace(tags, ", ", " #") as tags
  FROM #engineering OR #blockchain OR #design OR #communication OR #writing
  WHERE author != NULL
---