# Python_Day11
#Try-except Blocks, Common Python Exceptions
try:
    numerator = 10
    denominator = 0
    result = numerator / denominator
except ZeroDivisionError as e:
    print(f"An error occurred: {e}")
else:
    print(f"The result is {result}")
finally:
    print("Execution completed.")

    #Example Code for Signal Calculator:
def get_signal_input():
    """
    Prompt the user to enter signal readings and handle invalid inputs.
    
    Returns:
    list: A list of valid signal readings.
    """
    signal_readings = []
    while True:
        try:
            reading = float(input("Enter a signal reading (or type 'done' to finish): "))
            signal_readings.append(reading)
        except ValueError:
            user_input = input("Invalid input. Type 'done' to finish or press Enter to try again: ").strip().lower()
            if user_input == 'done':
                break
    return signal_readings

# Example usage:
readings = get_signal_input()
print(f"Valid signal readings: {readings}")

#Enhanced Log Analyzer Code:
def analyze_log(filename):
    """
    Analyze sensor log data from a text file with error handling.

    Parameters:
    filename (str): The name of the log file to analyze.

    Returns:
    dict: A dictionary containing the average, maximum, and minimum sensor readings.
    """
    readings = []
    try:
        with open(filename, 'r') as file:
            for line in file:
                try:
                    reading = float(line.strip().split('-')[-1])
                    readings.append(reading)
                except ValueError:
                    print(f"Invalid data found and skipped: {line.strip()}")
    except FileNotFoundError:
        print(f"Error: The file '{filename}' was not found.")
        return None
    except IOError:
        print(f"Error: An I/O error occurred while reading the file '{filename}'.")
        return None
    
    if readings:
        analysis = {
            'average': sum(readings) / len(readings),
            'max': max(readings),
            'min': min(readings)
        }
    else:
        analysis = {
            'average': None,
            'max': None,
            'min': None
        }
    
    return analysis

# Example usage:
log_file = 'sensor_log.txt'
results = analyze_log(log_file)
if results:
    print(f"Average reading: {results['average']}")
    print(f"Maximum reading: {results['max']}")
    print(f"Minimum reading: {results['min']}")
