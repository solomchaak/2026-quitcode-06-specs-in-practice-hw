# Здача WS6

## Дані

- Роль: pm
- Команда: property-workflows
- GitHub-логін: solomchaak
- Ваше репо: https://github.com/solomchaak/property-workflows-spec
- SHA: 4f886d8a9bf788b84fd58ff3d2c8b3b804585cd9
- Репо вимог PM: https://github.com/solomchaak/property-workflows-spec
- Прод-URL: —

## PM

- Сховище вимог: issues
- Продукт: https://github.com/solomchaak/property-workflows-spec/issues/1
- Вимоги першого зрізу: https://github.com/solomchaak/property-workflows-spec/issues/2, https://github.com/solomchaak/property-workflows-spec/issues/3
- Самоперевірка за чеклістом: https://github.com/solomchaak/property-workflows-spec/issues/2#issuecomment-6271860848, https://github.com/solomchaak/property-workflows-spec/issues/2#issuecomment-6295463177, https://github.com/solomchaak/property-workflows-spec/issues/3#issuecomment-6271861396, https://github.com/solomchaak/property-workflows-spec/issues/3#issuecomment-6295464896
- Питання, на які ви відповіли: https://github.com/solomchaak/property-workflows-spec/issues/4, https://github.com/solomchaak/property-workflows-spec/issues/5, https://github.com/solomchaak/property-workflows-spec/issues/6, https://github.com/solomchaak/property-workflows-spec/issues/7, https://github.com/solomchaak/property-workflows-spec/issues/8, https://github.com/solomchaak/property-workflows-spec/issues/9, https://github.com/solomchaak/property-workflows-spec/issues/10, https://github.com/solomchaak/property-workflows-spec/issues/11, https://github.com/solomchaak/property-workflows-spec/issues/12, https://github.com/solomchaak/property-workflows-spec/issues/13, https://github.com/solomchaak/property-workflows-spec/issues/14, https://github.com/solomchaak/property-workflows-spec/issues/15, https://github.com/solomchaak/property-workflows-spec/issues/16, https://github.com/solomchaak/property-workflows-spec/issues/17, https://github.com/solomchaak/property-workflows-spec/issues/18
- Зміни вимог із журналом змін: https://github.com/solomchaak/property-workflows-spec/issues/1#issuecomment-6271731738, https://github.com/solomchaak/property-workflows-spec/issues/1#issuecomment-6295214634, https://github.com/solomchaak/property-workflows-spec/issues/2#issuecomment-6271732307, https://github.com/solomchaak/property-workflows-spec/issues/2#issuecomment-6295215381, https://github.com/solomchaak/property-workflows-spec/issues/2#issuecomment-6295462738, https://github.com/solomchaak/property-workflows-spec/issues/3#issuecomment-6271732815, https://github.com/solomchaak/property-workflows-spec/issues/3#issuecomment-6295216061, https://github.com/solomchaak/property-workflows-spec/issues/3#issuecomment-6295464414

### Нотатка PM — порівняння реалізацій (трек D)

Шість розробників команди реалізували одні вимоги незалежно одне від одного. Посилання на код — на коміти `main` їхніх репо на 21.10: @dmudryk `63ed363e6ca2cc4d8a1ce830c04b4e43764bbbee`, @yuriivynar `0d3516a2224c0c1cfc8f79a83464a3f093703cd1`, @vsmrnk `e9e562feb4af05bfa4ddb7a8ac110a5c7d0fff26`, @OleksandrMartynov `1293dabf1283baef8e2ce33bfc3154c0584a3a1c`, @ylehenkyi-qc `56b509e244e47b5a0a6dbdd60d1b7e3bb5845911`, @vhrytsyndyshynquitcode `ab9e47dbc39cc6f9f87255a56eab574fc071d3b0`.

1. **AC / вимога:** AC-RUN-03 і припущення в https://github.com/solomchaak/property-workflows-spec/issues/2 — «Leading and trailing spaces are removed before the name is checked and saved; a name consisting only of spaces counts as empty».
   **Як прочитали чи реалізували:** слово «spaces» прочитали як різні множини символів.
   - @ylehenkyi-qc — лише символ пробілу: `input.replace(/^ +| +$/g, "")`, з коментарем «не будь-який whitespace» ([validateCaseName.ts#L9-L11](https://github.com/ylehenkyi-qc/property-workflows/blob/56b509e244e47b5a0a6dbdd60d1b7e3bb5845911/src/lib/runs/validateCaseName.ts#L9-L11)).
   - @dmudryk, @vhrytsyndyshynquitcode, @vsmrnk, @OleksandrMartynov — будь-який пробільний символ, через JavaScript `trim()` ([dmudryk rules.ts#L17](https://github.com/dmudryk/-property-workflows/blob/63ed363e6ca2cc4d8a1ce830c04b4e43764bbbee/src/lib/runs/rules.ts#L17), [vhrytsyndyshynquitcode domain.ts#L38](https://github.com/vhrytsyndyshynquitcode/property-workflows/blob/ab9e47dbc39cc6f9f87255a56eab574fc071d3b0/src/lib/runs/domain.ts#L38), [vsmrnk case-name.ts#L10](https://github.com/vsmrnk/property-workflows/blob/e9e562feb4af05bfa4ddb7a8ac110a5c7d0fff26/src/lib/runs/case-name.ts#L10), [OleksandrMartynov case-name.ts#L9](https://github.com/OleksandrMartynov/property-workflows/blob/1293dabf1283baef8e2ce33bfc3154c0584a3a1c/src/lib/runs/case-name.ts#L9)). У @vsmrnk і @OleksandrMartynov база при цьому обрізає лише пробіли (`btrim`), тож форма й база трактують назву з табуляцією по-різному.
   - @yuriivynar — те саме `trim()` у формі, але в базі помітив розрив і перестворив перевірку на той самий набір символів (включно з U+00A0) ([міграція, L3-L12](https://github.com/yuriivynar/property-workflows/blob/0d3516a2224c0c1cfc8f79a83464a3f093703cd1/supabase/migrations/20261020144507_case_name_whitespace_and_template_integrity.sql#L3-L12)).
   **Чому:** слово «spaces» не визначено в глосарії: символ пробілу чи будь-який пробільний символ (табуляція, нерозривний пробіл). Категорія: «Термінологія» (9) і «Граничні випадки» (7).
   **Що зробив PM:** залишив як є: у цьому зрізі назви з табуляцією чи нерозривним пробілом не очікуються (назви вводять менеджери вручну), а розбіжність не впливає на AC-RUN-03, AC-RUN-07 і AC-RUN-11. Якщо вимоги розширяться (наприклад, імпорт даних), уточню «spaces» як «будь-який пробільний символ».

2. **AC / вимога:** AC-TASK-04 і AC-TASK-16 у https://github.com/solomchaak/property-workflows-spec/issues/3 — «Marking the last required task of a run as done asks for confirmation … the task becomes "done" only after confirmation»; рішення PM у https://github.com/solomchaak/property-workflows-spec/issues/15.
   **Як прочитали чи реалізували:** підтвердження існує лише для останньої обов'язкової задачі, але хто його вимагає — по-різному.
   - База вимагає підтвердження (прямий виклик без нього відхиляється): @yuriivynar (параметр `p_confirmed`, [міграція, L1-L6](https://github.com/yuriivynar/property-workflows/blob/0d3516a2224c0c1cfc8f79a83464a3f093703cd1/supabase/migrations/20261021085138_mark_task_done_confirmation.sql#L1-L6); [actions.ts#L43-L46](https://github.com/yuriivynar/property-workflows/blob/0d3516a2224c0c1cfc8f79a83464a3f093703cd1/src/app/runs/%5Bid%5D/actions.ts#L43-L46)) і @OleksandrMartynov ([actions.ts#L62-L65](https://github.com/OleksandrMartynov/property-workflows/blob/1293dabf1283baef8e2ce33bfc3154c0584a3a1c/src/app/runs/actions.ts#L62-L65)).
   - Лише серверна дія застосунку (перенаправляє на підтвердження, але база прийме позначку без нього): @dmudryk ([actions.ts#L56-L60](https://github.com/dmudryk/-property-workflows/blob/63ed363e6ca2cc4d8a1ce830c04b4e43764bbbee/src/app/runs/actions.ts#L56-L60)) і @vhrytsyndyshynquitcode ([actions.ts#L43-L60](https://github.com/vhrytsyndyshynquitcode/property-workflows/blob/ab9e47dbc39cc6f9f87255a56eab574fc071d3b0/src/app/runs/actions.ts#L43-L60)).
   - Лише інтерфейс (кнопка питає, база не вимагає): @vsmrnk ([progress.ts#L30-L41](https://github.com/vsmrnk/property-workflows/blob/e9e562feb4af05bfa4ddb7a8ac110a5c7d0fff26/src/lib/runs/progress.ts#L30-L41), [mark-done-button.tsx#L8-L11](https://github.com/vsmrnk/property-workflows/blob/e9e562feb4af05bfa4ddb7a8ac110a5c7d0fff26/src/app/runs/%5Bid%5D/mark-done-button.tsx#L8-L11)).
   - Немає підтвердження: @ylehenkyi-qc (у репо немає жодного коду підтвердження; знімок вимог репо від 2026-10-19, до рішення PM).
   **Чому:** вимога каже, що користувач має підтвердити, але не каже, чи має це гарантувати саме застосунок, а чи й база, коли позначку надсилають поза інтерфейсом чи зі застарілої сторінки (@yuriivynar у міграції пояснює саме такий випадок). Категорія: «Потік взаємодії» (4) і «Граничні випадки» (7).
   **Що зробив PM:** відповів на питання про підтвердження (https://github.com/solomchaak/property-workflows-spec/issues/15): C, підтвердження лише для останньої обов'язкової задачі. Залишив на розсуд розробника: AC-TASK-04 і AC-TASK-16 перевіряють поведінку в інтерфейсі (підтвердження з назвою задачі й «This cannot be undone»). Жорсткіше рішення в базі (@yuriivynar, @OleksandrMartynov) підтримую, але не вимагаю від усіх. Якщо знадобиться гарантія незалежно від інтерфейсу, додам окремий AC у наступному оновленні.

3. **AC / вимога:** AC-RUN-04 і AC-RUN-02 («the run keeps the template exactly as it was at the moment of launch») у https://github.com/solomchaak/property-workflows-spec/issues/2.
   **Як прочитали чи реалізували:** що робити з призначенням для задачі, яку прибрали з шаблону, поки менеджер заповнював форму запуску.
   - @ylehenkyi-qc — запуск відхиляється з помилкою «Task does not belong to the template» ([міграція, L98-L103](https://github.com/ylehenkyi-qc/property-workflows/blob/56b509e244e47b5a0a6dbdd60d1b7e3bb5845911/supabase/migrations/20261020091927_launch_run_functions.sql#L98-L103)).
   - @OleksandrMartynov — спершу так само помилка (`INVALID_TASK`), а після відповіді PM призначення відкидається, запуск створюється ([міграція, L1-L4](https://github.com/OleksandrMartynov/property-workflows/blob/1293dabf1283baef8e2ce33bfc3154c0584a3a1c/supabase/migrations/20261021093026_launch_run_drop_stale_assignments.sql#L1-L4)).
   - @yuriivynar — ключ видаленої задачі ігнорується від початку, як «робоче рішення» ([міграція, L189-L192](https://github.com/yuriivynar/property-workflows/blob/0d3516a2224c0c1cfc8f79a83464a3f093703cd1/supabase/migrations/20261020115705_workflow_runs.sql#L189-L192)).
   **Чому:** «the moment of launch» у вимозі не прив'язаний ні до відкриття форми, ні до натискання «Launch». Категорія: «Граничні випадки й збої» (7).
   **Що зробив PM:** відповів на питання від @OleksandrMartynov (https://github.com/solomchaak/property-workflows-spec/issues/9): варіант A, момент запуску — підтвердження запуску, призначення для видаленої задачі відкидається, запуск не падає; додав це в «Припущення» вимоги https://github.com/solomchaak/property-workflows-spec/issues/2 з рядком журналу змін.

## Розробник

—

## Бонус E

—
