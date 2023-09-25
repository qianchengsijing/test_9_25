# test_9_25
#include <stdio.h>
#include <stdlib.h>

//双链表
typedef struct LNode{
	int data;
	struct LNode *next;
}LNode,*LinkList;
typedef struct DNode{
	int data;
	struct DNode *prior,*next;
}DNode,*DLinkList;
bool InitDLinkList(DLinkList &L){
	L = (DNode*)malloc(sizeof(DNode));
	if(L == NULL)
		return false;
	L->prior = NULL;
	L->next = NULL;
	return true;
}
bool LinkInsert(LinkList &L,int i,int e){
	if(i<1)
		return false;
	LNode* p;
	int j = 0;
	p = L;
	while(p != NULL && j<i-1){
		p = p->next;
		j++;
	}
	if(p != NULL)
		return false;
	LNode* s = (LNode*)malloc(sizeof(LNode));
	s->data = e;
	s->next = p->next;
	p->next = s;
	return true;
}
//指定结点后插
bool InsertNextDNode(DNode* p,DNode* s){
	if(p == NULL || s == NULL)
		return false;
	s->next = p->next;
	if(p->next != NULL)
		p->next->prior = s;
	s->prior = p;
	p->next = s;
	return true;
}
//删除结点
bool DeleteNextDNode(DNode* p){
	if(p == NULL)
		return false;
	DNode* q = p->next;
	if(q == NULL)
		return false;
	p->next = q->next;
	if(q->next != NULL)
		q->next->prior = p;
	free(q);
	return true;
}
//销毁链表
void DestoryList(DLinkList &L){
	while(L->next != NULL)
		DeleteNextDNode(L);
	free(L);
	L = NULL;
}
//循环单链表
bool InitList(LinkList &L){
	L = (LNode*)malloc(sizeof(LNode));
	if(L == NULL)
		return false;
	L->next = L;//单链表
	L->prior = L;//双链表
	return true;
}
bool Empty(LinkList L){
	if(L->next == L)
		return true;
	else
		return false;
}
bool Is_Tail(LinkList L，LNode* p){
	if(p->next == L)
		return true;
	else
		return false;
}
int main(){
	DLinkList L;
	InitDLinkList(L);
	return 0;
}
//静态链表
#define MaxSize 10
typedef struct{
	int data;
	int next;
}SLinkList[MaxSize];

void TestSLinkList(){
	SLinkList L;
	printf("size L=%d\n",sizeof(L));
	struct Node x;
	printf("size x=%d\n",sizeof(x));
	struct Node x[MaxSize];
	printf("size x[MaxSize]=%d\n",sizeof(x[MaxSize]));
}
int main(){
	TestSLinkList();
	return 0;
}
