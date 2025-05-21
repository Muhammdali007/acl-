#include <iostream>
#include <string>
#include <vector>
using namespace std;

// Structure to define an ACL rule
struct ACLRule {
    string sourceIP;
    string destinationIP;
    string port;
    bool permit;  // true = permit, false = deny
};

// Function to check if access is allowed based on ACL rules
bool isAccessAllowed(const vector<ACLRule>& acl, const string& srcIP, const string& dstIP, const string& port) {
    for (const auto& rule : acl) {
        if (rule.sourceIP == srcIP && rule.destinationIP == dstIP && rule.port == port) {
            return rule.permit;
        }
    }
    // Default deny if no rule matches
    return false;
}

int main() {
    // Sample ACL Rules
    vector<ACLRule> acl = {
        {"192.168.1.10", "192.168.2.20", "80", true},   // Allow HTTP
        {"192.168.1.10", "192.168.2.20", "23", false},  // Deny Telnet
        {"192.168.1.15", "192.168.3.30", "443", true}   // Allow HTTPS
    };

    // Simulate user input
    string srcIP, dstIP, port;
    cout << "Enter Source IP: ";
    cin >> srcIP;
    cout << "Enter Destination IP: ";
    cin >> dstIP;
    cout << "Enter Port (e.g., 80 for HTTP): ";
    cin >> port;

    // Check access
    if (isAccessAllowed(acl, srcIP, dstIP, port)) {
        cout << "Access PERMITTED based on ACL rules." << endl;
    } else {
        cout << "Access DENIED by ACL." << endl;
    }

    return 0;
} 
