===============================================================================
SQL joins
===============================================================================

SQL 有許多種 join，可以用集合的運算做類比。

假設現在有兩張 table A B，資料分別為::

  A     B
  +---+ +---+
  | a | | b |
  +===+ +===+
  | 1 | | 3 |
  | 2 | | 4 |
  | 3 | | 5 |
  | 4 | | 6 |
  +---+ +---+

* A inner join B 會產生 A B 的交集（intersection）::

    select * from A INNER JOIN B on A.a = B.b;

    +---+---+   .---------------------------.
    | a | b |   |                           |
    +---+---+   |         A       B         |
    | 3 | 3 |   |         .       .         |
    | 4 | 4 |   |       .' '.   .' '.       |
    +---+---+   |     .'     '.'     '.     |
                |   .'      .:::.      '.   |
                |  '.      ':::::'      .'  |
                |    '.      ':'      .'    |
                |      '.   .' '.   .'      |
                |        '.'     '.'        |
                |                           |
                '---------------------------'

* Outer join 分三種

  - A full outer join B 會產生 A B 的聯集（union），若其中一方沒有對應的值，則填 null::

      select * from a FULL OUTER JOIN b on a.a = b.b;

      +------+------+   .---------------------------.
      | a    | b    |   |                           |
      +======+======+   |         A       B         |
      | 1    | null |   |         .       .         |
      | 2    | null |   |       .:::.   .:::.       |
      | 3    | 3    |   |     .:::::::.:::::::.     |
      | 4    | 4    |   |   .:::::::::::::::::::.   |
      | null | 5    |   |  ':::::::::::::::::::::'  |
      | null | 6    |   |    ':::::::::::::::::'    |
      +------+------+   |      ':::::' ':::::'      |
                        |        ':'     ':'        |
                        |                           |
                        '---------------------------'

  - A left outer join B 會產生 A 的全部::

      select * from a LEFT OUTER JOIN b on a.a = b.b;

      +------+------+   .---------------------------.
      | a    | b    |   |                           |
      +======+======+   |         A       B         |
      | 1    | null |   |         .       .         |
      | 2    | null |   |       .:::.   .' '.       |
      | 3    | 3    |   |     .:::::::.'     '.     |
      | 4    | 4    |   |   .:::::::::::.      '.   |
      +------+------+   |  ':::::::::::::'      .'  |
                        |    ':::::::::'      .'    |
                        |      ':::::' '.   .'      |
                        |        ':'     '.'        |
                        |                           |
                        '---------------------------'

  - A right outer join B 會產生 B 的全部::

      select * from a RIGHT OUTER JOIN b on a.a = b.b;

      +------+------+   .---------------------------.
      | a    | b    |   |                           |
      +======+======+   |         A       B         |
      | 3    | 3    |   |         .       .         |
      | 4    | 4    |   |       .' '.   .:::.       |
      | null | 5    |   |     .'     '.:::::::.     |
      | null | 6    |   |   .'      .:::::::::::.   |
      +------+------+   |  '.      ':::::::::::::'  |
                        |    '.      ':::::::::'    |
                        |      '.   .' ':::::'      |
                        |        '.'     ':'        |
                        |                           |
                        '---------------------------'

Ref: https://stackoverflow.com/a/38578/3812388
