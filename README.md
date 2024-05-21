#<iostream>
#include <iomanip>

class Calendar {
private:
    int year;
    int month;

public:
    Calendar(int y, int m) : year(y), month(m) {}

    void display() {
        // Displaying the header
        std::cout << "==============================" << std::endl;
        std::cout << "       " << getMonthName() << " " << year << std::endl;
        std::cout << "==============================" << std::endl;
        std::cout << " Sun Mon Tue Wed Thu Fri Sat" << std::endl;

        // Getting the starting day of the month
        int startDay = getStartDay();

        // Printing the days
        for (int i = 0; i < startDay; ++i) {
            std::cout << "    ";
        }

        for (int day = 1; day <= getNumDays(); ++day) {
            std::cout << std::setw(4) << day;
            if ((startDay + day - 1) % 7 == 0) {
                std::cout << std::endl;
            }
        }
        std::cout << std::endl;
    }

private:
    bool isLeapYear() {
        return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
    }

    int getNumDays() {
        if (month == 2) {
            return isLeapYear() ? 29 : 28;
        } else if (month == 4 || month == 6 || month == 9 || month == 11) {
            return 30;
        } else {
            return 31;
        }
    }

    int getStartDay() {
        // Zeller's Congruence algorithm to find the day of the week
        int q = 1;
        int m = (month == 1 || month == 2) ? month + 12 : month;
        int K = year % 100;
        int J = year / 100;
        int h = (q + ((13 * (m + 1)) / 5) + K + (K / 4) + (J / 4) - (2 * J)) % 7;
        return (h + 6) % 7;
    }

    std::string getMonthName() {
        switch (month) {
            case 1: return "January";
            case 2: return "February";
            case 3: return "March";
            case 4: return "April";
            case 5: return "May";
            case 6: return "June";
            case 7: return "July";
            case 8: return "August";
            case 9: return "September";
            case 10: return "October";
            case 11: return "November";
            case 12: return "December";
            default: return "";
        }
    }
};

int main() {
    int year, month;
    std::cout << "Enter year: ";
    std::cin >> year;
    std::cout << "Enter month (1-12): ";
    std::cin >> month;

    Calendar cal(year, month);
    cal.display();

    return 0;
}

