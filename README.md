# tugasdatastruct
#include<stdio.h>
#include<stdlib.h>

struct tnode
{
	int x;
	tnode *next;
	tnode *prev;//1
}*head, *tail, *curr;

void push_front(int value)
{
	//create node
	struct tnode *node = (tnode*)malloc(sizeof(tnode));
	node->x = value;
	
	if(head==NULL)//cek data awal, jika tdk ada lgsg bikin node
	{
		head = tail = node;
		node->next = NULL;
		node->prev = NULL;//2
	}
	else
	{
		node->next = head;
		head->prev = node;//3
		head = node;
		head->prev = NULL;//4
	}
}

void push_back(int value)
{
	//create node
	struct tnode *node = (tnode*)malloc(sizeof(tnode));
	node->x = value;
	
	if(head==NULL)//cek data awal
	{
		head = tail = node;
		node->next = NULL;
		node->prev = NULL;
	}
	else
	{
		tail->next = node;
		node->prev = tail;
		tail = node;
		tail->next = NULL;
	}
}

void push_mid(int value, int searchKey)
{
	//create node
	struct tnode *node = (tnode*)malloc(sizeof(tnode));
	node->x = value;
	
	if(head==NULL)//cek data awal
	{
		head = tail = node;
		tail->next = NULL;
	}
	else
	{
		//struct tnode *curr = head;
		
		while(curr!=NULL)
		{
			if(curr->x == searchKey)
			{
				if(curr==tail)
				{
					push_back(value);
				}
				else
				{
					node->next = curr->next;
					curr->next = node;
				}
				break;
			}
			curr = curr->next;
		}
		if(curr==NULL)
		{
			printf("Data %d not found\n", searchKey);
		}
	}
}
void delete_front() {
    if (head == NULL) {
        printf("List is empty, nothing to delete.\n");
        return;
    }
    
    struct tnode *temp = head;
    head = head->next;
    
    if (head != NULL) {
        head->prev = NULL;
    } else {
        tail = NULL; 
    }
    free(temp);
}

void delete_back() {
    if (head == NULL) {
        printf("List is empty, nothing to delete.\n");
        return;
    }
    
    struct tnode *temp = tail;
    tail = tail->prev;
    
    if (tail != NULL) {
        tail->next = NULL;
    } else {
        head = NULL; 
    }
    free(temp);
}
void delete_mid(int searchKey)
{
    if (head == NULL) {
        printf("List is empty, nothing to delete.\n");
        return;
    }
    
    struct tnode *curr = head;
    
    while (curr != NULL) {
        if (curr->x == searchKey) {
        
            if (curr == head) {
                delete_front();
            }
        
            else if (curr == tail) {
                delete_back();
            }
        
            else {
                curr->prev->next = curr->next;
                curr->next->prev = curr->prev;
                free(curr);
            }
            return;
        }
        curr = curr->next;
    }

    printf("Data %d not found\n", searchKey);
}

//void clearData()
//{
//	while(head!=NULL)
//	{
//		curr = head;
//		head = head->next;
//		free(curr);
//	}
//}

void printList()
{
	if(head==NULL)
	{
		printf("There is No Data\n");
		return;
	}
	
	//struct tnode *curr = head;
	curr = head;
	
	while(curr!=NULL)
	{
		printf("%d ", curr->x);
		curr=curr->next;
	}
}


int main()
{
	printf("PUSH DATA\n");
	
	push_front(11);
	push_back(90);
	push_front(78);
	push_back(50);
	delete_front();
	delete_back();
	delete_mid(90);
	//78 11 90 50
	//push_mid(22,90);
	//push_mid(18,78);
	
	//50 78 90 11
	//78 11 90 50
	//78 18 11 90 22 50
	//printList();getchar();
//	clearData();
	printList();getchar();
	return 0;
}
