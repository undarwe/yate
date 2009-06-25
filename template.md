template
========

Стандартный синтаксис
---------------------

    template xpath {
        ...
    }

С модой
-------

    template xpath : mode {
        ...
    }

При этом можно использовать несколько xpath'ов и mode' через запятую или пайп:

    template xpath1, xpath2 : mode1, mode2 {
        ...
    }

Вложенные шаблоны
-----------------
Внутренний шаблон заматчится только если позван из внешнего.

    template xpath1 {
        ...

        template xpath2 {
            ...
        }
    }

Подшаблоны
----------
В этом случае xpath2 считается относительно xpath1.

    template xpath1 {
        ...

        subtemplate xpath2 {
            ...
        }
    }

Например:

    template / {
        apply message/subject // заматчится subtemplate subject
    }

    template message {
        ...
        apply subject // тоже заматчится subtemplate subject

        subtemplate subject {
            ...
        }
    }

Scope's
-------

    template / {
        apply message
    }

    template message {
        apply message/subject
    }

    {
        template message {
            apply subject
        }

        template message/subject {
            ... // #1
        }
    }

    template subject {
        ... // #2
    }


