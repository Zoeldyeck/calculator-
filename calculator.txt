import streamlit as st
import numpy as np

# Title for the calculator app
st.title("Streamlit Calculator")

# Sidebar for selecting basic or advanced mode
mode = st.sidebar.selectbox("Select Mode", ["Basic", "Advanced"])

if mode == "Basic":
    st.header("Basic Calculator")
    
    # Input fields for numbers
    num1 = st.number_input("Enter the first number:", value=0.0, step=0.1)
    num2 = st.number_input("Enter the second number:", value=0.0, step=0.1)

    # Selection of operation
    operation = st.selectbox("Select operation:", ["Addition", "Subtraction", "Multiplication", "Division"])

    # Perform the selected operation
    if operation == "Addition":
        result = num1 + num2
    elif operation == "Subtraction":
        result = num1 - num2
    elif operation == "Multiplication":
        result = num1 * num2
    elif operation == "Division":
        if num2 == 0:
            st.error("Division by zero is not allowed.")
            result = None
        else:
            result = num1 / num2
    
    # Display the result
    if result is not None:
        st.write(f"The result of {operation.lower()} is: {result}")

elif mode == "Advanced":
    st.header("Advanced Calculator")
    
    # Select advanced operation
    advanced_operation = st.selectbox("Select operation:", ["Square Root", "Exponentiation", "Sine", "Cosine", "Tangent", "Logarithm"])

    if advanced_operation in ["Sine", "Cosine", "Tangent"]:
        # Input for trigonometric operations (angles in degrees)
        angle = st.number_input("Enter the angle in degrees:", value=0.0)
        radians = np.radians(angle)
        
        if advanced_operation == "Sine":
            result = np.sin(radians)
        elif advanced_operation == "Cosine":
            result = np.cos(radians)
        elif advanced_operation == "Tangent":
            result = np.tan(radians)
        st.write(f"The result of {advanced_operation.lower()}({angle}°) is: {result}")
    
    else:
        # Input field for other operations
        num = st.number_input("Enter a number:", value=0.0)

        if advanced_operation == "Square Root":
            if num < 0:
                st.error("Square root of a negative number is not real.")
            else:
                result = np.sqrt(num)
                st.write(f"The square root of {num} is: {result}")
        
        elif advanced_operation == "Exponentiation":
            exponent = st.number_input("Enter the exponent:", value=1.0)
            result = np.power(num, exponent)
            st.write(f"{num} raised to the power of {exponent} is: {result}")

        elif advanced_operation == "Logarithm":
            if num <= 0:
                st.error("Logarithm is not defined for non-positive numbers.")
            else:
                result = np.log(num)
                st.write(f"The natural logarithm of {num} is: {result}")

# Footer
st.sidebar.info("This calculator supports basic and advanced operations.")
