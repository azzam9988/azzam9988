- 👋 Hi, I’m @azzam9988
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
azzam9988/azzam9988 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
#include <stdio.h>
#include <stdlib.h>

// Define the structure for a queue node
struct Node {
    int data;
    struct Node* next;
};

// Define the structure for the queue
struct Queue {
    struct Node *front, *rear;
};

// Function to create a new node
struct Node* newNode(int data) {
    struct Node* temp = (struct Node*)malloc(sizeof(struct Node));
    temp->data = data;
    temp->next = NULL;
    return temp;
}

// Function to create an empty queue
struct Queue* createQueue() {
    struct Queue* q = (struct Queue*)malloc(sizeof(struct Queue));
    q->front = q->rear = NULL;
    return q;
}

// Function to add an item to the queue
void enqueue(struct Queue* q, int data) {
    struct Node* temp = newNode(data);

    // If queue is empty, then new node is both front and rear
    if (q->rear == NULL) {
        q->front = q->rear = temp;
        return;
    }

    // Add the new node at the end of the queue and change rear
    q->rear->next = temp;
    q->rear = temp;
}

// Function to remove an item from the queue
void dequeue(struct Queue* q) {
    // If queue is empty, return NULL
    if (q->front == NULL)
        return;

    // Store previous front and move front one node ahead
    struct Node* temp = q->front;
    q->front = q->front->next;

    // If front becomes NULL, then change rear also as NULL
    if (q->front == NULL)
        q->rear = NULL;

    free(temp);
}

// Function to display the queue
void displayQueue(struct Queue* q) {
    struct Node* temp = q->front;
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

// Main function to test the FIFO queue implementation
int main() {
    struct Queue* q = createQueue();
    enqueue(q, 10);
    enqueue(q, 20);
    enqueue(q, 30);

    printf("Queue after enqueues: ");
    displayQueue(q);

    dequeue(q);
    printf("Queue after one dequeue: ");
    displayQueue(q);

    dequeue(q);
    printf("Queue after another dequeue: ");
    displayQueue(q);

    return 0;
}
