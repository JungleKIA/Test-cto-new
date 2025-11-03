# Comprehensive Javadoc Guide (English)

## Table of Contents
1. [General Principles and Structure](#1-general-principles-and-structure)
2. [Documenting Classes, Interfaces, and Enums](#2-documenting-classes-interfaces-and-enums)
3. [Documenting Methods and Constructors](#3-documenting-methods-and-constructors)
4. [Block Tags Usage](#4-block-tags-usage)
5. [Inline Tags Usage](#5-inline-tags-usage)
6. [Good vs Bad Examples](#6-good-vs-bad-examples)
7. [Common Mistakes and Best Practices Checklist](#7-common-mistakes-and-best-practices-checklist)

---

## 1. General Principles and Structure

### 1.1 Summary Sentence Rule

The first sentence of every Javadoc comment is the **summary sentence**. It must:
- Be a complete, grammatically correct sentence
- End with a period (`.`), exclamation mark (`!`), or question mark (`?`)
- Provide a concise overview of the documented element
- Appear in summary listings and search results

**Rules:**
- The summary sentence ends at the first period followed by a space, tab, or line terminator
- Use `{@literal .}` if you need a period that doesn't end the summary
- Keep it concise (ideally under 80 characters)

**Example:**
```java
/**
 * Calculates the factorial of a given number. This method uses
 * an iterative approach for better performance.
 *
 * @param n the number to calculate factorial for
 * @return the factorial result
 */
public long factorial(int n) {
    // implementation
}
```

### 1.2 Main Description

After the summary sentence, provide a detailed description:
- Use multiple sentences to explain functionality, behavior, and context
- Separate paragraphs with `<p>` tags
- Use lists (`<ul>`, `<ol>`) for structured information
- Keep descriptions focused on **what** the code does, not **how**

**Example:**
```java
/**
 * Manages user authentication and session tracking.
 * <p>
 * This class provides methods to:
 * <ul>
 *   <li>Authenticate users against multiple identity providers</li>
 *   <li>Manage session lifecycle and timeout</li>
 *   <li>Handle password reset workflows</li>
 * </ul>
 * <p>
 * All methods in this class are thread-safe and can be called
 * from multiple threads concurrently.
 */
public class AuthenticationManager {
    // implementation
}
```

### 1.3 Safe HTML Tag Usage

**Allowed HTML tags** (most common):
- Paragraphs: `<p>`, `</p>`
- Lists: `<ul>`, `<ol>`, `<li>`
- Text formatting: `<b>`, `<i>`, `<strong>`, `<em>`, `<code>`
- Line breaks: `<br>`
- Tables: `<table>`, `<tr>`, `<td>`, `<th>`
- Headings: `<h1>` through `<h6>`
- Links: `<a href="...">`

**Important rules:**
- Always close tags properly (`<p>...</p>`)
- Use `{@code ...}` instead of `<code>` for Java code snippets
- Don't use deprecated HTML tags (`<font>`, `<center>`, etc.)

### 1.4 Special Character Escaping

Special characters that need escaping:
- `<` → use `&lt;` or `{@literal <}`
- `>` → use `&gt;` or `{@literal >}`
- `&` → use `&amp;` or `{@literal &}`
- `@` → use `{@literal @}` (when not used as a tag)

**Example:**
```java
/**
 * Compares two values using the {@literal <} operator.
 * Returns true if {@code a < b}, false otherwise.
 *
 * @param a the first value
 * @param b the second value
 * @return true if a is less than b
 */
public boolean isLessThan(int a, int b) {
    return a < b;
}
```

---

## 2. Documenting Classes, Interfaces, and Enums

### 2.1 Purpose Description

Every class, interface, and enum must have Javadoc that explains:
- **What** it represents or does
- **Why** it exists (its role in the system)
- **When** to use it
- Key constraints or assumptions

### 2.2 Usage Examples

Include code examples for complex classes or when usage isn't immediately obvious:

```java
/**
 * A builder for creating immutable {@link UserProfile} instances.
 * <p>
 * This builder provides a fluent API for constructing user profiles
 * with validation and default values.
 * <p>
 * Example usage:
 * <pre>{@code
 * UserProfile profile = new UserProfileBuilder()
 *     .withUsername("john.doe")
 *     .withEmail("john@example.com")
 *     .withRole(Role.ADMIN)
 *     .build();
 * }</pre>
 *
 * @author Jane Smith
 * @version 2.0
 * @since 1.5
 */
public class UserProfileBuilder {
    // implementation
}
```

### 2.3 Required and Recommended Tags

**Required tags:**
- `@author` - Author name(s), one tag per author
- `@version` - Current version identifier
- `@since` - Version when this element was introduced

**Recommended tags:**
- `@see` - References to related classes or external documentation
- `@deprecated` - If the class is deprecated (always suggest alternative)

**Example:**
```java
/**
 * Represents a connection to a legacy database system.
 * <p>
 * This class is deprecated in favor of {@link ModernDatabaseConnection}
 * which provides better performance and connection pooling.
 *
 * @author John Doe
 * @author Jane Smith
 * @version 3.2.1
 * @since 1.0
 * @see ModernDatabaseConnection
 * @deprecated since 3.0, use {@link ModernDatabaseConnection} instead
 */
@Deprecated
public class LegacyDatabaseConnection {
    // implementation
}
```

### 2.4 Interfaces

Document interfaces with focus on contract and expectations:

```java
/**
 * Defines the contract for data persistence operations.
 * <p>
 * Implementations of this interface must ensure that:
 * <ul>
 *   <li>All operations are atomic</li>
 *   <li>Failed operations throw specific exceptions</li>
 *   <li>Null values are handled according to method documentation</li>
 * </ul>
 *
 * @author Jane Smith
 * @version 2.0
 * @since 1.0
 */
public interface DataRepository {
    // method declarations
}
```

### 2.5 Enums

Document enums with focus on each constant's meaning:

```java
/**
 * Defines the possible states of a user account.
 * <p>
 * These states control what operations a user can perform
 * and how the system interacts with the account.
 *
 * @author John Doe
 * @version 1.2
 * @since 1.0
 */
public enum AccountStatus {
    
    /**
     * Account is active and user can perform all operations.
     */
    ACTIVE,
    
    /**
     * Account is temporarily suspended due to security reasons.
     * User cannot log in until status changes to {@link #ACTIVE}.
     */
    SUSPENDED,
    
    /**
     * Account is pending email verification.
     * Limited operations are available in this state.
     */
    PENDING_VERIFICATION,
    
    /**
     * Account has been permanently closed by user or administrator.
     * This state is irreversible.
     */
    CLOSED
}
```

---

## 3. Documenting Methods and Constructors

### 3.1 Describe What, Not How

Focus on the method's contract and behavior, not implementation details:

**Bad:**
```java
/**
 * Loops through the array and adds each element to a sum variable.
 */
public int calculateSum(int[] numbers) {
    // implementation
}
```

**Good:**
```java
/**
 * Calculates the sum of all elements in the given array.
 *
 * @param numbers the array of numbers to sum, must not be null
 * @return the sum of all elements, or 0 if array is empty
 * @throws NullPointerException if numbers is null
 */
public int calculateSum(int[] numbers) {
    // implementation
}
```

### 3.2 Side Effects and Behavior Specifics

Always document:
- Thread safety characteristics
- Modifications to parameters or object state
- Network or I/O operations
- Long-running operations
- Caching behavior

**Example:**
```java
/**
 * Sends an email notification to the specified recipient.
 * <p>
 * This method performs network I/O and may block for several seconds.
 * Consider calling from a background thread for better responsiveness.
 * <p>
 * This method is thread-safe and can be called concurrently from
 * multiple threads.
 *
 * @param recipient the email address of the recipient, must not be null or empty
 * @param subject the email subject line, must not be null
 * @param body the email body content, must not be null
 * @throws IllegalArgumentException if recipient is not a valid email address
 * @throws EmailServiceException if the email cannot be sent due to network
 *         or service errors
 */
public void sendEmail(String recipient, String subject, String body) {
    // implementation
}
```

### 3.3 Detailed @param Documentation

Each `@param` tag must:
- Describe what the parameter represents
- Specify constraints (null/not null, range, format)
- Explain the parameter's role in the operation

**Example:**
```java
/**
 * Creates a new user account with the specified details.
 *
 * @param username the unique username for the account, must not be null,
 *                 must be between 3 and 20 characters, and contain only
 *                 alphanumeric characters and underscores
 * @param email the user's email address, must not be null and must be
 *              a valid email format
 * @param age the user's age in years, must be between 13 and 150 (inclusive)
 * @return the newly created user account with generated ID
 * @throws IllegalArgumentException if any parameter violates its constraints
 * @throws DuplicateUsernameException if the username is already taken
 */
public UserAccount createUser(String username, String email, int age) {
    // implementation
}
```

### 3.4 Clear @return Documentation

Document the return value including:
- What it represents
- Possible special values (null, empty, -1, etc.)
- Edge cases
- When null or empty might be returned

**Example:**
```java
/**
 * Searches for a user by their username.
 *
 * @param username the username to search for, must not be null or empty
 * @return the user account if found, or null if no user exists with
 *         the given username
 * @throws IllegalArgumentException if username is null or empty
 */
public UserAccount findUserByUsername(String username) {
    // implementation
}

/**
 * Retrieves all active user accounts.
 *
 * @return an unmodifiable list of active users, empty if no active
 *         users exist, never null
 */
public List<UserAccount> getActiveUsers() {
    // implementation
}
```

### 3.5 Comprehensive @throws Documentation

Document **all** exceptions that the method can throw:
- **Checked exceptions**: must be documented
- **Unchecked exceptions**: should be documented if they're part of the contract
- Include the **condition** that causes each exception

**Example:**
```java
/**
 * Processes a payment transaction.
 *
 * @param accountId the account to charge, must not be null
 * @param amount the payment amount, must be positive
 * @param currency the currency code (e.g., "USD", "EUR"), must not be null
 * @return the transaction receipt with confirmation number
 * @throws NullPointerException if accountId or currency is null
 * @throws IllegalArgumentException if amount is zero or negative, or if
 *         currency is not a valid ISO 4217 code
 * @throws AccountNotFoundException if no account exists with the given ID
 * @throws InsufficientFundsException if the account balance is less than
 *         the requested amount
 * @throws PaymentProcessingException if the payment cannot be processed
 *         due to a system error
 */
public Receipt processPayment(String accountId, BigDecimal amount, String currency)
        throws AccountNotFoundException, InsufficientFundsException,
               PaymentProcessingException {
    // implementation
}
```

### 3.6 Constructor Documentation

Document constructors similarly to methods:

```java
/**
 * Creates a new shopping cart for the specified user.
 * <p>
 * The cart is initialized empty and ready to accept items.
 *
 * @param userId the ID of the user who owns this cart, must not be null
 * @param sessionId the current session identifier, must not be null or empty
 * @throws NullPointerException if userId is null
 * @throws IllegalArgumentException if sessionId is null or empty
 */
public ShoppingCart(String userId, String sessionId) {
    // implementation
}

/**
 * Creates a new shopping cart with pre-populated items.
 * <p>
 * This constructor is useful for restoring carts from persistent storage.
 *
 * @param userId the ID of the user who owns this cart, must not be null
 * @param sessionId the current session identifier, must not be null or empty
 * @param items the initial items in the cart, must not be null but can be empty
 * @throws NullPointerException if any parameter is null
 * @throws IllegalArgumentException if sessionId is empty
 */
public ShoppingCart(String userId, String sessionId, List<CartItem> items) {
    // implementation
}
```

---

## 4. Block Tags Usage

### 4.1 Standard Block Tags

Block tags must appear after the main description and follow strict ordering:

**Standard order:**
1. `@author` (classes and interfaces only)
2. `@version` (classes and interfaces only)
3. `@param` (methods and constructors)
4. `@return` (methods only)
5. `@throws` or `@exception` (methods and constructors)
6. `@see`
7. `@since`
8. `@deprecated`

### 4.2 @param

Used for method and constructor parameters, and type parameters:

```java
/**
 * Stores a key-value pair in the cache.
 *
 * @param <K> the type of keys maintained by this cache
 * @param <V> the type of mapped values
 * @param key the key with which the specified value is to be associated,
 *            must not be null
 * @param value the value to be associated with the specified key,
 *              null values are allowed
 * @throws NullPointerException if key is null
 */
public <K, V> void put(K key, V value) {
    // implementation
}
```

### 4.3 @return

Used to describe the return value of methods (not constructors):

```java
/**
 * Calculates the average of the given numbers.
 *
 * @param numbers the array of numbers to average, must not be null or empty
 * @return the arithmetic mean of all numbers in the array
 * @throws IllegalArgumentException if numbers is null or empty
 */
public double calculateAverage(double[] numbers) {
    // implementation
}
```

**Note:** Omit `@return` for void methods.

### 4.4 @throws / @exception

Documents exceptions that may be thrown:

```java
/**
 * Reads the contents of a file.
 *
 * @param filePath the path to the file to read, must not be null
 * @return the file contents as a string, never null
 * @throws NullPointerException if filePath is null
 * @throws FileNotFoundException if the file does not exist
 * @throws IOException if an I/O error occurs during reading
 * @throws SecurityException if a security manager exists and denies
 *         read access to the file
 */
public String readFile(Path filePath) throws IOException {
    // implementation
}
```

**Note:** `@throws` and `@exception` are synonymous; use `@throws` for consistency.

### 4.5 @see

Creates links to related elements:

```java
/**
 * Encrypts sensitive data using AES-256 algorithm.
 *
 * @param plaintext the data to encrypt, must not be null
 * @param key the encryption key, must be exactly 32 bytes
 * @return the encrypted data
 * @throws NullPointerException if plaintext or key is null
 * @throws IllegalArgumentException if key length is not 32 bytes
 * @see #decrypt(byte[], byte[])
 * @see EncryptionUtils
 * @see <a href="https://en.wikipedia.org/wiki/Advanced_Encryption_Standard">AES on Wikipedia</a>
 */
public byte[] encrypt(byte[] plaintext, byte[] key) {
    // implementation
}
```

### 4.6 @since

Indicates when an element was added:

```java
/**
 * Validates an email address using RFC 5322 rules.
 *
 * @param email the email address to validate, must not be null
 * @return true if the email is valid, false otherwise
 * @since 2.1
 */
public boolean isValidEmail(String email) {
    // implementation
}
```

### 4.7 @deprecated

Marks deprecated elements and suggests alternatives:

```java
/**
 * Calculates a hash code using MD5 algorithm.
 *
 * @param input the input string, must not be null
 * @return the MD5 hash
 * @deprecated since 3.0, MD5 is cryptographically broken. Use
 *             {@link #calculateSHA256(String)} instead
 */
@Deprecated
public String calculateMD5(String input) {
    // implementation
}

/**
 * Calculates a hash code using SHA-256 algorithm.
 *
 * @param input the input string, must not be null
 * @return the SHA-256 hash
 * @since 3.0
 */
public String calculateSHA256(String input) {
    // implementation
}
```

---

## 5. Inline Tags Usage

Inline tags can appear anywhere in the description or block tag comments.

### 5.1 {@code}

Used for code snippets, keywords, and identifiers:
- Displays text in monospace font
- Disables HTML interpretation
- No need to escape HTML special characters inside

**Example:**
```java
/**
 * Checks if the collection contains the specified element.
 * <p>
 * This method returns {@code true} if this collection contains at least
 * one element {@code e} such that {@code Objects.equals(o, e)}.
 *
 * @param element the element to search for
 * @return {@code true} if element is found, {@code false} otherwise
 */
public boolean contains(Object element) {
    // implementation
}
```

### 5.2 {@literal}

Similar to `{@code}` but displays in normal font (not monospace):
- Disables HTML interpretation
- Use for displaying special characters without code semantics

**Example:**
```java
/**
 * Compares two strings lexicographically.
 * <p>
 * Returns a negative integer if {@literal this < that}, zero if
 * {@literal this == that}, or a positive integer if {@literal this > that}.
 *
 * @param other the string to compare with
 * @return comparison result
 */
public int compareTo(String other) {
    // implementation
}
```

### 5.3 {@link} and {@linkplain}

Creates hyperlinks to other documented elements:
- `{@link}` displays in monospace (code font)
- `{@linkplain}` displays in normal font

**Syntax:**
- `{@link ClassName}` - link to class
- `{@link ClassName#methodName}` - link to method
- `{@link ClassName#methodName(Type)}` - link to specific overload
- `{@link #methodName}` - link to method in current class
- `{@link ClassName label text}` - custom link text

**Example:**
```java
/**
 * A specialized list implementation.
 * <p>
 * This class extends {@link java.util.ArrayList} and provides additional
 * functionality for bulk operations. For standard list operations, see
 * {@link java.util.List}.
 * <p>
 * Use {@link #addAll(Collection)} for efficient bulk insertion, or
 * {@linkplain #addOne(Object) the single-element add method} for
 * individual elements.
 *
 * @param <E> the type of elements in this list
 * @see java.util.ArrayList
 * @see java.util.List
 */
public class EnhancedList<E> extends ArrayList<E> {
    // implementation
}
```

### 5.4 {@value}

Displays the value of a constant:

**Example:**
```java
/**
 * Configuration constants for the application.
 */
public class AppConfig {
    
    /**
     * The maximum number of retry attempts.
     * Value: {@value}
     */
    public static final int MAX_RETRIES = 3;
    
    /**
     * The default timeout in milliseconds.
     * Value: {@value}
     */
    public static final long DEFAULT_TIMEOUT = 5000L;
    
    /**
     * The application version string.
     * Value: {@value}
     */
    public static final String VERSION = "2.1.0";
}

/**
 * Attempts to connect with automatic retries.
 * <p>
 * This method will retry up to {@value AppConfig#MAX_RETRIES} times
 * with a timeout of {@value AppConfig#DEFAULT_TIMEOUT} milliseconds.
 *
 * @return true if connection succeeds, false otherwise
 */
public boolean connect() {
    // implementation
}
```

### 5.5 {@inheritDoc}

Copies documentation from an overridden method or implemented interface:

```java
public interface DataSource {
    /**
     * Opens a connection to the data source.
     *
     * @return a new connection instance
     * @throws ConnectionException if the connection cannot be established
     */
    Connection open() throws ConnectionException;
}

public class DatabaseDataSource implements DataSource {
    /**
     * {@inheritDoc}
     * <p>
     * This implementation uses connection pooling for better performance.
     */
    @Override
    public Connection open() throws ConnectionException {
        // implementation
    }
}
```

---

## 6. Good vs Bad Examples

### 6.1 Class Documentation

#### ❌ Bad Example

```java
/**
 * User service.
 */
public class UserService {
    public void addUser(String name, String email) {
        // implementation
    }
}
```

**Problems:**
- No summary sentence ending with period
- Missing `@author`, `@version`, `@since` tags
- Too brief, no useful information
- Method not documented

#### ✅ Good Example

```java
/**
 * Provides business logic for managing user accounts.
 * <p>
 * This service handles user creation, retrieval, updates, and deletion
 * operations. It enforces business rules such as username uniqueness
 * and email validation.
 * <p>
 * All methods are thread-safe and transactional.
 *
 * @author Jane Smith
 * @version 2.1.0
 * @since 1.0.0
 * @see UserRepository
 * @see UserValidator
 */
public class UserService {
    
    /**
     * Adds a new user to the system.
     * <p>
     * This method validates the input parameters, checks for username
     * and email uniqueness, and persists the new user account.
     *
     * @param name the full name of the user, must not be null or empty
     * @param email the email address, must not be null and must be valid
     * @return the created user with generated ID
     * @throws NullPointerException if name or email is null
     * @throws IllegalArgumentException if name is empty or email is invalid
     * @throws DuplicateEmailException if the email is already registered
     */
    public User addUser(String name, String email) {
        // implementation
    }
}
```

### 6.2 Method with Complex Logic

#### ❌ Bad Example

```java
/**
 * Processes order
 * @param order
 * @return result
 */
public boolean processOrder(Order order) {
    // implementation
}
```

**Problems:**
- Summary sentence doesn't end with period
- No detailed description
- Parameter description missing
- Return value not explained
- Missing exception documentation
- No information about side effects

#### ✅ Good Example

```java
/**
 * Processes a customer order through the complete fulfillment pipeline.
 * <p>
 * This method performs the following operations:
 * <ol>
 *   <li>Validates the order contents and customer information</li>
 *   <li>Checks inventory availability for all items</li>
 *   <li>Reserves inventory and creates shipping labels</li>
 *   <li>Processes payment through the payment gateway</li>
 *   <li>Updates order status to PROCESSING</li>
 * </ol>
 * <p>
 * If any step fails, all previous operations are rolled back and
 * the order status is set to FAILED.
 * <p>
 * This method performs network I/O and database transactions, so
 * it may take several seconds to complete. It is thread-safe and
 * can handle concurrent order processing.
 *
 * @param order the order to process, must not be null and must have
 *              at least one item and valid customer information
 * @return {@code true} if the order was successfully processed and
 *         payment confirmed, {@code false} if processing failed for
 *         any reason
 * @throws NullPointerException if order is null
 * @throws IllegalStateException if the order has already been processed
 *         or cancelled
 * @throws ValidationException if order data is invalid or incomplete
 * @throws InventoryException if any items are out of stock
 * @throws PaymentException if payment processing fails
 */
public boolean processOrder(Order order) throws ValidationException,
                                                 InventoryException,
                                                 PaymentException {
    // implementation
}
```

### 6.3 Fixing Common doclint Errors

#### ❌ Bad: Missing @param Tag

```java
/**
 * Calculates the total price.
 *
 * @return the total price
 */
public double calculateTotal(double price, double taxRate) {
    // implementation
}
```

**doclint error:** `error: @param for "price" not found`, `error: @param for "taxRate" not found`

#### ✅ Good: All Parameters Documented

```java
/**
 * Calculates the total price including tax.
 *
 * @param price the base price before tax, must be non-negative
 * @param taxRate the tax rate as a decimal (e.g., 0.08 for 8%), must
 *                be between 0 and 1
 * @return the total price including tax
 * @throws IllegalArgumentException if price is negative or taxRate is
 *         outside the valid range
 */
public double calculateTotal(double price, double taxRate) {
    // implementation
}
```

#### ❌ Bad: Incorrect HTML

```java
/**
 * Formats the text with <b>bold formatting.
 * <p>Uses the <br> tag.
 *
 * @param text the input text
 * @return formatted text
 */
public String formatText(String text) {
    // implementation
}
```

**doclint errors:**
- `error: element not closed: b`
- `error: self-closing element not allowed`

#### ✅ Good: Proper HTML

```java
/**
 * Formats the text with <b>bold formatting</b>.
 * <p>
 * Uses the line break tag where needed.
 *
 * @param text the input text, must not be null
 * @return the formatted text with HTML markup, never null
 * @throws NullPointerException if text is null
 */
public String formatText(String text) {
    // implementation
}
```

#### ❌ Bad: Invalid Reference

```java
/**
 * Processes data.
 *
 * @see DataProcessor#process(Data)
 * @param data the input
 * @return result
 */
public Result processData(Object data) {
    // implementation
}
```

**doclint error:** `error: reference not found: DataProcessor#process(Data)`

#### ✅ Good: Valid References

```java
/**
 * Processes input data and produces a result.
 *
 * @param data the input data to process, must not be null
 * @return the processing result containing status and output data,
 *         never null
 * @throws NullPointerException if data is null
 * @see DataProcessor#process(java.lang.Object)
 */
public Result processData(Object data) {
    // implementation
}
```

#### ❌ Bad: Dangling Javadoc

```java
/**
 * This is a dangling comment.
 */

public class MyClass {
    // implementation
}
```

**doclint error:** `error: no comment`

#### ✅ Good: Attached Javadoc

```java
/**
 * Represents a custom class for demonstration purposes.
 *
 * @author John Doe
 * @version 1.0
 * @since 1.0
 */
public class MyClass {
    // implementation
}
```

### 6.4 Complete Working Example

```java
package com.example.service;

import java.util.List;
import java.util.Optional;

/**
 * Manages inventory operations for products in the warehouse.
 * <p>
 * This service provides comprehensive inventory management including:
 * <ul>
 *   <li>Stock level tracking and updates</li>
 *   <li>Automatic reorder point notifications</li>
 *   <li>Multi-warehouse support</li>
 *   <li>Transaction history and audit trails</li>
 * </ul>
 * <p>
 * All operations are transactional and thread-safe. The service
 * maintains consistency across concurrent modifications using
 * optimistic locking.
 *
 * @author Jane Smith
 * @author John Doe
 * @version 3.2.1
 * @since 1.0.0
 * @see Product
 * @see Warehouse
 * @see InventoryTransaction
 */
public class InventoryService {
    
    /**
     * The minimum stock level before reorder alert is triggered.
     * Value: {@value}
     */
    public static final int DEFAULT_REORDER_POINT = 10;
    
    /**
     * Retrieves the current stock level for a product.
     * <p>
     * This method queries all warehouses and returns the aggregate
     * stock level. The result is cached for 5 minutes to improve
     * performance.
     *
     * @param productId the unique identifier of the product, must not
     *                  be null or empty
     * @return the total stock level across all warehouses, or 0 if
     *         the product is not found
     * @throws IllegalArgumentException if productId is null or empty
     */
    public int getStockLevel(String productId) {
        // implementation
        return 0;
    }
    
    /**
     * Updates the stock level for a product in a specific warehouse.
     * <p>
     * This method adds or removes stock and creates an audit trail
     * entry. If the new stock level falls below the reorder point,
     * a notification is sent to the purchasing department.
     * <p>
     * The operation is atomic and uses optimistic locking to prevent
     * concurrent modification conflicts.
     *
     * @param productId the unique identifier of the product, must not
     *                  be null or empty
     * @param warehouseId the warehouse identifier, must not be null or empty
     * @param quantity the quantity to add (positive) or remove (negative),
     *                 must not result in negative stock
     * @param reason the reason for the stock change (e.g., "sale", "return",
     *               "adjustment"), must not be null or empty
     * @return the new stock level after the update
     * @throws IllegalArgumentException if any parameter is invalid or if
     *         the operation would result in negative stock
     * @throws ProductNotFoundException if no product exists with the given ID
     * @throws WarehouseNotFoundException if no warehouse exists with the
     *         given ID
     * @throws ConcurrentModificationException if another transaction modified
     *         the stock level concurrently
     * @see #getStockLevel(String)
     */
    public int updateStock(String productId, String warehouseId,
                          int quantity, String reason) {
        // implementation
        return 0;
    }
    
    /**
     * Finds products with stock levels below their reorder points.
     * <p>
     * This method scans all products and returns those that need
     * to be reordered. The default reorder point is
     * {@value #DEFAULT_REORDER_POINT} units, but each product can
     * have a custom reorder point.
     *
     * @return an unmodifiable list of products needing reorder, empty
     *         if all products have sufficient stock, never null
     */
    public List<Product> findProductsNeedingReorder() {
        // implementation
        return List.of();
    }
    
    /**
     * Retrieves the complete transaction history for a product.
     * <p>
     * This method returns all stock movements (additions and removals)
     * for the specified product, ordered by timestamp descending (most
     * recent first).
     *
     * @param productId the unique identifier of the product, must not
     *                  be null or empty
     * @return an optional containing the list of transactions if the
     *         product exists, or an empty optional if the product is
     *         not found
     * @throws IllegalArgumentException if productId is null or empty
     * @see InventoryTransaction
     */
    public Optional<List<InventoryTransaction>> getTransactionHistory(
            String productId) {
        // implementation
        return Optional.empty();
    }
}
```

---

## 7. Common Mistakes and Best Practices Checklist

### 7.1 Common doclint Errors

#### Missing Elements

- [ ] **Missing Javadoc comment**: Every public/protected class, interface, enum, method, and constructor must have Javadoc
- [ ] **Missing summary sentence**: First sentence must end with period, exclamation, or question mark
- [ ] **Missing @param tag**: Every parameter must be documented
- [ ] **Missing @return tag**: Every non-void method must have @return
- [ ] **Missing @throws tag**: All declared exceptions and important runtime exceptions must be documented

#### HTML Errors

- [ ] **Unclosed HTML tags**: All tags must be properly closed (e.g., `<p>...</p>`, `<b>...</b>`)
- [ ] **Invalid self-closing tags**: Use `<br>` not `<br/>` in HTML4 mode
- [ ] **Bad HTML entities**: Use `&lt;`, `&gt;`, `&amp;` or `{@literal}` for special characters
- [ ] **Deprecated HTML tags**: Avoid `<font>`, `<center>`, etc.

#### Reference Errors

- [ ] **Invalid @see reference**: Ensure referenced classes and methods exist and are fully qualified if needed
- [ ] **Invalid {@link} reference**: Check spelling and include parameter types for overloaded methods
- [ ] **Broken external links**: Verify URLs in `<a href="...">` tags

#### Structure Errors

- [ ] **Wrong tag order**: Follow standard order (author, version, param, return, throws, see, since, deprecated)
- [ ] **Dangling Javadoc**: Ensure comment is directly attached to the element without blank lines
- [ ] **Javadoc on wrong element**: Don't put class-level tags on methods or vice versa

### 7.2 Best Practices Checklist

#### Writing Style

- [ ] Use **present tense** (e.g., "Returns the user" not "Will return the user")
- [ ] Use **third person** (e.g., "Calculates the sum" not "Calculate the sum")
- [ ] Start method descriptions with a **verb** (e.g., "Validates", "Creates", "Retrieves")
- [ ] Be **concise** but **complete** - include all necessary information without redundancy
- [ ] Avoid **implementation details** - describe what, not how

#### Content

- [ ] Document **preconditions** (what must be true before calling)
- [ ] Document **postconditions** (what will be true after calling)
- [ ] Document **side effects** (state changes, I/O operations, etc.)
- [ ] Document **thread safety** for concurrent code
- [ ] Document **null handling** (can parameters be null? Can return be null?)
- [ ] Document **empty cases** (empty collections, zero values, etc.)
- [ ] Include **usage examples** for complex APIs

#### Parameters and Returns

- [ ] Every @param must explain **what** the parameter is and **constraints** on its value
- [ ] Use "must not be null" or "can be null" for every reference parameter
- [ ] Specify **ranges** for numeric parameters (e.g., "must be positive", "between 0 and 100")
- [ ] Explain special @return values (null, empty, -1, etc.)
- [ ] Use "never null" or "can be null" for return values

#### Exceptions

- [ ] Document **all checked exceptions** in throws clause
- [ ] Document **important runtime exceptions** (NullPointerException, IllegalArgumentException, etc.)
- [ ] Explain the **condition** that causes each exception
- [ ] Use specific exception types, not generic Exception

#### Tags and Links

- [ ] Use `{@code}` for code elements (keywords, class names, variables)
- [ ] Use `{@link}` for references to other documented elements
- [ ] Use `{@literal}` for special characters in regular text
- [ ] Include `@see` links to related classes and methods
- [ ] Mark deprecated elements with both `@deprecated` tag and `@Deprecated` annotation
- [ ] Always suggest **alternatives** in @deprecated comments

#### Validation Commands

Before committing, validate your Javadoc:

```bash
# Generate Javadoc with doclint enabled
javadoc -Xdoclint:all -d target/javadoc -sourcepath src/main/java \
    -subpackages com.example

# With Maven
mvn javadoc:javadoc -Djavadoc.lint=all

# With Gradle
./gradlew javadoc -Pjavadoc.lint=all
```

### 7.3 Quick Reference: Tag Order

For **classes and interfaces**:
```
@author
@version
@param (for type parameters)
@see
@since
@deprecated
```

For **methods and constructors**:
```
@param (all parameters)
@return (methods only)
@throws (all exceptions)
@see
@since
@deprecated
```

### 7.4 Pre-Commit Checklist

Before committing code with Javadoc:

1. [ ] All public/protected elements have Javadoc
2. [ ] All summary sentences end with proper punctuation
3. [ ] All parameters are documented
4. [ ] All exceptions are documented
5. [ ] HTML tags are properly closed
6. [ ] Links and references are valid
7. [ ] No doclint warnings or errors
8. [ ] Code examples compile and run
9. [ ] Spelling and grammar are correct
10. [ ] Documentation matches actual behavior

---

## Conclusion

This guide provides comprehensive coverage of Javadoc best practices that comply with `doclint` requirements. Following these guidelines will ensure your API documentation is:

- **Complete**: All elements properly documented
- **Accurate**: Documentation matches implementation
- **Consistent**: Uniform style and structure
- **Professional**: Meets Oracle standards
- **Maintainable**: Easy to update as code evolves

Remember: Good documentation is as important as good code. Invest the time to write clear, complete Javadoc comments - your future self and your colleagues will thank you!
