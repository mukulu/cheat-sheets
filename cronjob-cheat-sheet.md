# Cronjob Writing rules

## CRONTAB FILE

Location: `/etc/crontab`

Below is the format of the cronjob file in relation to its commands.

| \# minute | \# hour | \# dayOfMonth | \# month | \# dayOfWeek | \# user | \# command                                              |
|-----------|---------|----------------|----------|---------------|---------|--------------------------------------------------------|
| *         | *       | *              | *        | *             | *       | command  \#runs command every minute                   |
| 1         | *       | *              | *        | *             | *       | command  \#run every 1st minute of an hour            |
| */2       | *       | *              | *        | *             | *       | command  \#run after every 2 minutes                   |
| 5         | 0       | *              | *        | *             | *       | command  \#runs 5mins after midnight every day         |
| 15        | 14      | 1              | *        | *             | *       | command  \#runs at 14:15 on 1st of every month        |
| 0         | 22      | *              | *        | 1-5          | *       | command  \#runs 22:00 on week days                     |
| 23        | 0-23/2  | *              | *        | *             | *       | command  \#runs 00:23, 02:23, 04:23, 06:23 and so on  |
| 5         | 4       | *              | *        | sun           | *       | command  \#runs 04:05 every sunday                     |
| 30        | */3     | *              | *        | 6-7          | *       | command  \#runs 00:30, 03:30, 06:30 and so on for weekends |

> **Note:** The user column is optional (usually ignored to be determined by user account cronjob).

Cron jobs can also be edited with: ```crontab -e```

## Field Allowed Values

| Field          | Allowed Values   |
|----------------|------------------|
| minute         | 0-59             |
| hour           | 0-23             |
| day of month   | 1-31             |
| month          | 1-12 (or names)  |
| day of week    | 0-7 (0 or 7 is Sun, or use names) |

- A field may be an asterisk (`*`), which stands for "first to last" or "all".
- Ranges of numbers are allowed. Ranges are two numbers separated with a hyphen. The specified range is inclusive. For example, `8-11` specifies execution at hours 8, 9, 10, and 11.
- Lists are allowed. A list is a set of numbers (or ranges) separated by commas. Examples: `1,2,5,9`, `0-4,8-12`.
- Step values can be used in conjunction with ranges. Following a range with `/<number>` specifies skips of the number's value through the range. For example, `0-23/2` specifies command execution every other hour.
- Steps are also permitted after an asterisk, so if you want to say "every two hours", just use `*/2`.
- Names can also be used for the "month" and "day of week" fields. Use the first three letters of the particular day or month (case doesn’t matter). Ranges or lists of names are not allowed.

## Special Strings

Instead of the first five fields, one of eight special strings may appear:

| String      | Meaning                              |
|-------------|--------------------------------------|
| `@reboot`   | Run once, at startup.                |
| `@yearly`   | Run once a year, "0 0 1 1 *".       |
| `@annually` | (same as `@yearly`)                  |
| `@monthly`  | Run once a month, "0 0 1 * *".      |
| `@weekly`   | Run once a week, "0 0 * * 0".       |
| `@daily`    | Run once a day, "0 0 * * *".        |
| `@midnight` | (same as `@daily`)                   |
| `@hourly`   | Run once an hour, "0 * * * *".      |

## Presenting Text for Reading

To present text for reading, use the following syntax:

```bash
more << "EOF"
Your text goes
all the way over here
when it ends EOF follows
EOF