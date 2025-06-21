# Windows Security internals

## FOREWORD

## ACKNOWLEDGMENTS

## INTROCUCTION

- Who Is This Book For?
- What is in This Book?
- PowerShell Conventions Userd in This Book
- Getting in touch

## PART1 : AN OVERVIEW OF THE WINDOWS OPERATING SYSTEM

### 1. SETTING UP A POWERSHELL TESTING ENVIRONMENT

- Choosing a PowerShell Version
- Configuring PowerShell
- An verview of the PowerShell Language
  - Understainding Types,Variavbles, and Expressions
  - Executing Commands
  - Discovering Commands and Getting Help
  - Defining Functions
  - Displaying and Manipulating Objects
  - Filtering,Ordering and Grouping Objects
  - Exporting Data
- Wrapping Up

### 2. THE WINDOWS KERNEL

- The Windows Kernel Executive
- The Security Reference Monitor
- The Object Manager
  - Object Types
  - The ObjectManager Namespace
  - System Calls
  - NTSTATUS Codes
  - Object Handles
  - Query and Set Information System Calls
- The Input/Output Manager
- The Process and Thread Manager
- The Memory Manager
  - NtVirtualMemory Commands
  - Section Objects
- Code Integrity
- advanced Local Procedure Call
- The Configuration Manager
- Worked Examples
  - Finding Open Handles by Name
  - Finding Shared Objects
  - Modfying a mapped Section
  - Finding Writable and Executable Memory
- Wrapping Up

### 3. USER-MODE APPLICATIONS

- win32 and User-Mode Windows APIs
  - Loading a New Library
  - Viewing Impoted APIs
  - Searching for DLLs
- The Win32 GUI
  - GUI Kernel Resources
  - Windows Messages
  - Console Sessions
- Comparing Win32 APIs and System Calls
- Win32 Registry Path
  - Opening Keys
  - Listing the Registry's Contents
- DOS Device Paths
  - Path Types
  - Maximum Path Length
- Process Creation
  - Command Line Parsing
  - Shell APIs
- System Processes
  - The Session Manager
  - The Windows Logon Process
  - The Local Security Authority Subsystem
  - The Service Control Manager
- Worked Example
  - Finding Executables That Important specific APIs
  - Finding Hidden Registry Keys or Values
- Wrapping Up

## PART2 : THE WINDOWS SECURITY REFERENCE MONITOR

### 4. SECURITY ACCESS TOKENS

- Primary Tokens
- Impersonation Tokens
  - Security Quality of service
  - Explicit Token Impersonation
- Converting Between Token Types
- Pseudo Token Handles
- Token Groups
  - Enabled,EnabledByDefault, and Mandatory
  - LogonId
  - Owner
  - UseForDenyOnly
  - Integrity and Integrityenabled
  - resource
  - Device Groups
- Privileges
- Sandbox Tokens
  - Restricted Tokens
  - Write-restricted Tokens
  - AppContainer and Lowbox Tokens
- What Makes and Administrator User?
- User Account Control
  - Linked Tokens and Elevation Type
  - UI Access
  - Virtualization
- Security Attributes
- Creating Tokens
- Token Assignment
  - Assigning a primary Token
  - Assigning an Impersonation Token
- Worked Examples
  - Finding UI Access Processes
  - Finding Token Handles to Impersonate
  - Removing Administrator Privileges
- Wrapping Up

### 5. SECURITY DESCRIPTORS

- The structure of a security Descriptor
- The Structure of a SID
- Absolute and Relative Security Descriptors
- Access Control List Headers and Entries
  - The Header
  - The ACE List
- Constructing and Manipulating Security Descriptors
  - Creating a New Security Descriptor
  - Ordering the ACEs
  - Formatting Security Descriptors
  - Converting to and from a Relative Security Descriptor
- The Security Descriptor Definition Language
- Worked Examples
  - Manually Parsing a Binary SID
  - Enumerating SIDs
- Wrapping Up

### 6. READING AND ASSIGNING SECURITY DESCRIPTORS

- Reading Security Descritors
- Assigning Security Descriptors
  - Assigning a Security Descriptor During Resource Creation
  - Assigning a Security Descriptor to an Existing Resource
- Win32 Security APIs
- Server Security Descriptors and Compound ACEs
- A Summary of Inheritance Behaivior
- worked Examples
  - Finding Object Manager Resource Owners
  - Changing the Ownership of a Resource
- Wrapping Up

### 7. THE ACCESS CHECK PROCESS

- Running an Access Check
  - Kernel-Mode Access Checks
  - User-Mode Access Checks
  - The Get-NtGrantedAccess PowerShellCommand
- The Access Check Process in PowerShell
  - Defining the Access Check Function
  - Performing the Mandary Access Check
  - Performing the Token Access Check
  - Performing the Discretionary Access Check
- Sandboxing
  - Restricted Tokens
  - Lowbox Tokens
- Enterprise Access Checks
  - The Object Type Access Check
  - The CentralAccess Policy
- Worked Examples
  - Using the Get-PSGrantedAccess Command
  - Calculating Granted Access for Resouces
- Wrapping Up

### 8. OTHER ACCESS CHECKING USE CASES

- Traversal Checking
  - The SeChangeNotifyPrivilege Privilege
  - Limited Checks
- Handle Duplication Access Checks
- Sandbox Token Checks
- Automating Access Checks
- Worked Examples
  - Simplifying an Access Check for an Object
  - Finding Writable Section Objects
- Wrapping Up

### 9. SECURITY AUDITING

- The Security Event Log
  - Configuring the Systen Audit Policy
  - Configuring the Per-User Audit POlicy
- Audit Policy Security
  - Configuring the Resource SACL
  - Configuring the Global SACL
- Worked Examples
  - Verifying Audit Access Seurity
  - Finding Resources with Audit ACEs
- Wrapping Up

## PART3: THE LOCAL SECURITY AUTHRITY AND AUTHENTICATION

### 10. WINDOWS AUTHENTICATION

- Domain Authentication
  - Local Authentication
  - Enterprise Network Domains
  - Domain Forests
- Local Domain Configration
  - The User Database
  - The LSA Policy Database
- Remote LSA Services
  - The SAM Remote Services
  - The Domain Policy Remote Service
- The SAM and SECURITY Databeses
  - Accessing the SAM Database Through the Registry
  - Inspecting the SECURITY Database
- Worked Examples
  - RID Cycling
  - Forcing a User's PAssword Change
  - Extracting All Local User Hashes
- Wrapping Up

### 11. ACTIVE DIRECTORY

- A Breif History of Active Directory
- Exploring an Active Directory Domain with PowerShell
  - The Remote Server Administration Tools
  - Basic Forest and Domain Information
  - The Users
  - The Groups
  - The Computers
- Objects and Distinguished Name
  - Enumerating Directory Objects
  - Accessing Objets in Other Domains
- The Schema
  - inspecting the Schema
  - Accessing the Security Attributes
- Security Descriptors
  - Querying Security Descriptors of Direcroty Objects
  - Assigning Security Descriptors to New Directory Objects
  - Assigning Security Descriptors to Existing Objects
  - Inspecting a Security Descriptor's Inherited Security
- Access Checks
  - Creating Objects
  - Deleting Objects
  - Listing Objects
  - Reading and Writing Attributes
  - Checking Multiple Attributes
  - Analyzing Property Sets
  - Inspecting Control Access Rights
  - Analyzing Write-Validated Access Rights
  - Accessing the SELF SID
  - Perfoming Additional Security Checks
- Claims and Central Access Policies
- Group Policies
- Worked Examples
  - Building the Authorization Context
  - Gathering Object Information
  - Running the Access Check
- Wrapping Up

### 12. INTERACTIVE AUTHENTICATION

- Creating a User's Desktop
- The LsaLogonUser API
  - Local Authentication
  - Domain Authentication
  - Logon and Console Sessions
  - Token Creation
- Using the LsaLogonUser API from PowerShell
- Creating a New Process with a Token
- The Service Logon Type
- Worked Examples
  - Testing Privileges and Logon Account Rights
  - Creating a Process in a Different Console Session
  - Authenticating Virtual Accounts
- Wrapping Up

### 13. NETWORJ AUTHENTICATION

- NTLM Network Authentication
  - NTLM Authentication Using PowerShell
  - The Cryptographic Derivation Process
  - Pass-Through Authentication
  - Local Loopback Authentication
  - Alternative Client Credentials
- The NTLM Relay Attack
  - Attack Overview
  - Active Server Challenges
  - Signing and Sealing
  - Target Names
  - Channel Binding
- Worked Examples
  - Overview
  - TheCode Module
  - The Server Implementation
  - The Client Implementation
  - The NTLM Authentication Test
- Wrapping Up

### 14. KERBEROS

- Interactive Authetication with Kerberos
  - Initial User Authentication
  - Network Service Authentication
- Perfoming Kerberos Authentication in PowerShell
- Decrypting the AP-REQ Message
- Decrypting the AP-REP Message
- Cross-Domain Authentication
- Kerberos Delegation
  - Unconstrained Delegation
  - Constrained Delegation
- User-to-User Kerberos Authentication
- Worked Examples
  - Querying the Kerberos Ticket Chache
  - Simple Kerberoasting
- Wrapping Up

### 15. NEGOTIATE AUTHENTICATION AND OTHER SECURITY PACKAGES

- Security Buffers
  - Using Buffers with an Authentication Context
  - Using Buffers with Signing and Sealing
- The Negotiate Protocol
- Less Common Security Packages
  - Secure Channel
  - CredSSP
- Remote Creadential Guard and Restricted Admin Mode
- The Credential Manager
- Additional Request Attribute Flags
  - Anonymous Sessions
  - Identity Tokens
- Network Autehntication with a Lowbox Token
  - Authentication with the Enterprise Authentication Capability
  - Authentication to a Known Web Proxy
  - Authentication with Explicit Credentials
- The Authenstication Audit Event Log
- Worked Examples
  - Identifying the Reason for an Authentication Failure
  - Using Secure Channel to Extract a Server's TLS Certificate
- Wrapping Up
- Final Thoughts

## A : BUILDING A WINDOWS DOMAIN NETWORK FOR TESTING

- The Domain Network
- Installing and Configuring Windows Hyper-V
- Creating the Virtual Machines
  - The PRIMARYDC Server
  - The GRAPHITE Workstation
  - The SALESDC Server

## B : SDDL SID ALIAS MAPPING

## INDEX
