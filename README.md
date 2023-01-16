# Linked Lists

This project is an implementation of a linked list data structure. Each node in the list contains a single element of data and a pointer to the next node in the list. The project uses a factory function for creating the nodes and a class for the linked list itself.

```javascript
function node() {
  let value = null;
  let next = null;

  return { value, next };
}

class LinkedList {
  constructor() {
    this.firstNode = null;
    this.lastNode = null;
    this.length = 0;
  }

  append(value) {
    const newNode = node();
    newNode.value = value;

    if (this.lastNode) {
      this.lastNode.next = newNode;
    }

    if (!this.firstNode) {
      this.firstNode = newNode;
    }

    this.lastNode = newNode;

    this.length += 1;
  }

  prepend(value) {
    const newNode = node();
    newNode.value = value;

    if (this.firstNode) {
      newNode.next = this.firstNode;
    }

    if (!this.lastNode) {
      this.lastNode = newNode;
    }

    this.firstNode = newNode;

    this.length += 1;
  }

  size() {
    return this.length;
  }

  head() {
    return this.firstNode;
  }

  tail() {
    return this.lastNode;
  }

  at(index) {
    let currentPosition = this.firstNode;

    for (let i = 0; i < this.length; i++) {
      if (index === i) {
        return currentPosition;
      } else {
        currentPosition = currentPosition.next;
      }
    }

    return null;
  }

  pop() {
    if (!this.length) {
      return;
    }

    if (this.length === 1) {
      this.firstNode = null;
      this.lastNode = null;

      return;
    }

    const beforeLast = this.at(this.length - 2);
    beforeLast.next = null;
    this.lastNode = beforeLast;

    this.length -= 1;
  }

  contains(value) {
    let currentPosition = this.firstNode;

    while (currentPosition) {
      if (currentPosition.value === value) {
        return true;
      }

      currentPosition = currentPosition.next;
    }

    return false;
  }

  find(value) {
    let index = 0;
    let currentPosition = this.firstNode;

    while (currentPosition) {
      if (currentPosition.value === value) {
        return index;
      }

      currentPosition = currentPosition.next;

      index += 1;
    }

    return null;
  }

  toString() {
    let currentString = "";
    let currentPosition = this.firstNode;

    while (currentPosition) {
      currentString += `(${currentPosition.value}) -> `;

      if (!currentPosition.next) {
        currentString += "null";
      }

      currentPosition = currentPosition.next;
    }

    return currentString;
  }

  insertAt(value, index) {
    if (index < 0 || index > this.length) {
      return;
    }

    if (index === 0) {
      this.prepend(value);
      return;
    }

    if (index === this.length) {
      this.append(value);
      return;
    }

    const prevNode = this.at(index - 1);
    const nextNode = this.at(index);

    const newNode = node();
    newNode.value = value;

    prevNode.next = newNode;
    newNode.next = nextNode;

    this.length += 1;
  }

  removeAt(index) {
    if (index < 0 || index >= this.length) {
      return;
    }

    if (index === 0) {
      this.firstNode = this.firstNode.next;
      this.length -= 1;
      return;
    }

    const nodeToRemove = this.at(index);
    const prevNode = this.at(index - 1);

    prevNode.next = nodeToRemove.next;

    this.length -= 1;
  }
}
```
