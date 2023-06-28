# Evaluate-a-postfix-expression-using-stack
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, item):
        self.stack.append(item)

    def pop(self):
        if not self.is_empty():
            return self.stack.pop()
        return None

    def is_empty(self):
        return len(self.stack) == 0


def evaluate_postfix(expression):
    stack = Stack()

    operators = set(['+', '-', '*', '/'])

    for char in expression:
        if char not in operators:
            stack.push(int(char))
        else:
            operand2 = stack.pop()
            operand1 = stack.pop()
            if operand1 is None or operand2 is None:
                raise ValueError("Invalid postfix expression")

            if char == '+':
                result = operand1 + operand2
            elif char == '-':
                result = operand1 - operand2
            elif char == '*':
                result = operand1 * operand2
            elif char == '/':
                result = operand1 / operand2
            stack.push(result)

    final_result = stack.pop()

    if stack.is_empty() and final_result is not None:
        return final_result
    else:
        raise ValueError("Invalid postfix expression")

postfix_exp = "523*+"
result = evaluate_postfix(postfix_exp)
print("Result:", result)
