#include <stdio.h>
#include <conio.h>
#include <windows.h>

#define MAPH 20
#define MAPW 40
#define SPACEBAR 32
#define GRAVITY 1


int main()
{
    char map[MAPH][MAPW];
    int nkey;
    int trigg = 1;


    for (int i = 0; i < MAPH; i++)
    {
        for (int j = 0; j < MAPW; j++)
        {
            if ((i == 0) || (i == MAPH - 1))
                map[i][j] = '#';
            else if ((j == 0) ||  (j == MAPW - 1))
                map[i][j] = '#';
            else
                map[i][j] = '.';

        }
    }
    for (int i = 20; i < MAPW; i++)
        map[15][i] = '#';

    for (int i = 0; i < MAPH; i++)
    {
        for (int j = 0; j < MAPW; j++)
        {
            printf("%c", map[i][j]);
        }
        printf("\n");
    }

    while (!(_kbhit()))
    {
        system("cls");
        printf("아무키 입력하여 시작");
        Sleep(100);
    }

    int cur_x = 3, cur_y =10, jump = 0;
    while (1)
    {
        if (_kbhit())
        {
            nkey = _getch();
            if (nkey == 'e')
                break;
            else if (nkey == 100)
            {
                if (map[cur_y][cur_x + 1] == '#')
                    continue;
                cur_x = cur_x + 1;
                map[cur_y][cur_x] = 'o';
                map[cur_y][cur_x - 1] = '.';
            }
            else if (nkey == 'a')
            {
                if (map[cur_y][cur_x - 1] == '#')
                    continue;
                cur_x = cur_x - 1;
                map[cur_y][cur_x] = 'o';
                map[cur_y][cur_x + 1] = '.';
            }

            else if (nkey == SPACEBAR)
            {
                jump = 4;
                for (int i = 0; i < MAPW; i++)
                {
                    if ((i == 0) || (i == MAPW - 1))
                        map[18][i] = '#';
                    else
                        map[18][i] = '.';
                }
            }

        }



        system("cls");
        for (int i = 0; i < MAPH; i++)
        {
            for (int j = 0; j < MAPW; j++)
            {
                printf("%c", map[i][j]);
            }
            printf("\n");
        }
       

        Sleep(10);

        if (map[cur_y + 1][cur_x] != '#')
        {
            cur_y++;
            map[cur_y][cur_x] = 'o';
            map[cur_y - 1][cur_x] = '.';
        }
        if (jump > 0)
        {
            cur_y -= jump;
            jump -= 1;
            if (jump < 0)
            {
                map[cur_y + jump][cur_x] = '.';
                map[cur_y][cur_x] = 'o';
                
            }
            map[cur_y + jump][cur_x] = '.';
            map[cur_y][cur_x] = 'o';

        }
            
            

    }
    return 0;
}
