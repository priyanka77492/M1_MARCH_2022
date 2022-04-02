#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <windows.h>

struct student{
    char stud_id[15];
    char stud_name[20];
    char stud_address[20];
    char stud_parentName[20];
    int stud_class;
    int stud_contact_number;
};

struct student stu;

void SetColor(int ForgC)
{
     WORD wordcolor;
     HANDLE studentHandleOutput = GetStdHandle(STD_OUTPUT_HANDLE);
     CONSOLE_SCREEN_BUFFER_INFO conscrbufinfo;
     if(GetConsoleScreenBufferInfo(studentHandleOutput, &conscrbufinfo))
     {
          wordcolor = (conscrbufinfo.wAttributes & 0xF0) + (ForgC & 0x0F);
          SetConsoleTextAttribute(studentHandleOutput, wordcolor);
     }
     return;
}

void ClearConsoleToColors(int ForgC, int BackC)
{
     WORD wordColor = ((BackC & 0x0F) << 4) + (ForgC & 0x0F);

     HANDLE studentHandleOutput = GetStdHandle(STD_OUTPUT_HANDLE);

     COORD coordinates = {0, 0};

     DWORD counting;

     CONSOLE_SCREEN_BUFFER_INFO conscrbufinfo;

     SetConsoleTextAttribute(studentHandleOutput, wordColor);
     if(GetConsoleScreenBufferInfo(studentHandleOutput, &conscrbufinfo))
     {

          FillConsoleOutputCharacter(studentHandleOutput, (TCHAR) 32, conscrbufinfo.dwSize.X * conscrbufinfo.dwSize.Y, coordinates, &counting);
          FillConsoleOutputAttribute(studentHandleOutput, conscrbufinfo.wAttributes, conscrbufinfo.dwSize.X * conscrbufinfo.dwSize.Y, coordinates, &counting );

          SetConsoleCursorPosition(studentHandleOutput, coordinates);
     }
     return;
}

void Setting_Color_And_Background(int ForgC, int BackC)
{
     WORD wordColor = ((BackC & 0x0F) << 4) + (ForgC & 0x0F);;
     SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), wordColor);
     return;
}

COORD coordinates = {0,0};
void x_and_y_coordinates(int x, int y){
    coordinates.X = x; coordinates.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coordinates);
}
