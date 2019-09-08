# My-Test
我的项目仓库
include <stdio.h>
#include <string.h>
 
#define ARRAY_LEN 30
 
/*联系人结构体*/
/*注：本程序忽略重名现象。若重名则查找时以最后输入的联系人为准。*/
typedef struct{
    char name[10];
    int age;
    char sex[10];
    char mp[13];
    char tel[13];
} friend_list;
 
/*打印所有联系人信息*/
void printAll (friend_list friList[], int *friNum) {
    int i;
     
    if (*friNum) {
        printf ("姓名\t\t年龄\t\t性别\t\t手机\t\t家庭\n");
        for (i=0; i<*friNum; i++)
            printf ("%s\t\t%d\t\t%s\t\t%s\t\t%s\n",friList[i].name,friList[i].age,friList[i].sex,friList[i].mp,friList[i].tel);
        printf ("\n");
    }
    else {
        printf ("无任何联系人信息！\n");
        printf ("\n");
    }
 
}
 
/*打印联系人信息*/
void printFri (friend_list friList[], int index) {
     
    if (index==-1) {
        printf ("查无此人！\n");
        printf ("\n");
    }
    else {
        printf ("姓名\t\t年龄\t\t性别\t\t手机\t\t家庭\n");
        printf ("%s\t\t%d\t\t%s\t\t%s\t\t%s\n",friList[index].name,friList[index].age,friList[index].sex,friList[index].mp,friList[index].tel);
        printf ("\n");
    }
}
 
/*按姓名定位联系人所在数组位置*/
int findIndex (friend_list friList[], int *friNum, char *tarName) {
    int i,index;
    index =-1;
     
    for (i=0; i<*friNum; i++)
        if (strcmp(tarName, friList[i].name) == 0) /*两字符串相等strcmp函数返回0*/
            index = i; /*定位联系人在结构体数组中的下标*/
     
    return index;
}
 
/*录入联系人信息*/
void addFri (friend_list friList[], int *friNum) {
    int i = *friNum;
     
    printf ("请输入联系人信息：\n");
    printf ("姓名：");
    scanf ("%s",&friList[i].name); 
    printf ("年龄：");
    scanf ("%d",&friList[i].age);
    printf ("性别：");
    scanf ("%s",&friList[i].sex);
    printf ("手机：");
    scanf ("%s",&friList[i].mp);
    printf ("家庭：");
    scanf ("%s",&friList[i].tel);
     
    *friNum +=1; /*联系人数加1*/
     
    printf ("\n");
}
 
/*按姓名查找联系人信息*/
void findFri (friend_list friList[], int *friNum) {
    int i,index;
    char tarName[10];
     
    printf ("请输入欲查找的联系人姓名：");
    scanf ("%s",&tarName);
    printf ("\n");
 
    index = findIndex (friList, friNum, tarName);
    printFri (friList, index); /*打印联系人信息*/
}
 
/*删除联系人信息*/
void delFri (friend_list friList[], int *friNum) {
    int i,index;
    char tarName[10];
     
    printf ("请输入欲删除的联系人姓名：");
    scanf ("%s",&tarName);
    printf ("\n");
 
    index = findIndex (friList, friNum, tarName);
     
    if (index == -1) {
        printf ("查无此人！\n");
        printf ("\n");
    }
    else {
        for (i=index; i<*friNum; i++)
            friList[i] = friList[i+1]; 
        *friNum-=1;
        printf ("联系人%s已删除！\n",tarName);
        printf ("\n");
    }
}
 
/*修改联系人信息*/
void altFri (friend_list friList[], int *friNum) {
    int index;
    char tarName[10];
     
    printf ("请输入欲修改的联系人姓名：");
    scanf ("%s",&tarName);
    printf ("\n");
 
    index = findIndex (friList, friNum, tarName);
 
    if (index == -1) {
        printf ("查无此人！\n");
        printf ("\n");
    }
    else {
        printf ("请重新输入联系人信息：\n");
        printf ("姓名：%s\n",friList[index].name);
        printf ("年龄：");
        scanf ("%d",&friList[index].age);
        printf ("性别：");
        scanf ("%s",&friList[index].sex);
        printf ("手机：");
        scanf ("%s",&friList[index].mp);
        printf ("家庭：");
        scanf ("%s",&friList[index].tel);
     
        printf ("联系人%s信息已修改！\n",tarName);
        printf ("\n");
    }
}
 
/*打印菜单*/
void printMenu (void) {
        printf ("======================================================\n\n");
        printf ("序号\t功能详情\n");
        printf ("1\t新增联系人\n");
        printf ("2\t按姓名查找联系人\n");
        printf ("3\t按姓名删除联系人\n");
        printf ("4\t按姓名修改联系人\n");
        printf ("5\t列出所有联系人信息\n");
        printf ("6\t退出\n");
        printf ("\n");
        printf ("======================================================\n\n");
}
 
/*输入命令*/
int instructions (void) {
    int key;
     
    printf ("请输入功能序号以开启操作：");
    scanf ("%d",&key);
    printf ("\n");
    printf ("======================================================\n\n");
     
    return key;
}
 
int main(void) {
    int key;
 
    int friNum = 0; /*联系人数量*/
    friend_list friList[ARRAY_LEN]; /*联系人结构体数组*/
 
    do {
        printMenu ();
         
        key = instructions ();
         
        switch (key){
            case 1: addFri (friList, &friNum); break;
            case 2: findFri (friList, &friNum); break;
            case 3: delFri (friList, &friNum); break;
            case 4: altFri (friList, &friNum); break;
            case 5: printAll (friList, &friNum); break;
            case 6: printf("程序结束！\n\n"); break;
            default: printf("输入错误，请重新输入！\n\n");break;
        }
        if (key!=6) {
            printf("按回车键继续\n");getchar ();getchar ();
        }
    } while(key!=6);
    return 0;
}
