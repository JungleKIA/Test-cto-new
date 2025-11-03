# Javadoc Documentation Guidelines

This repository contains comprehensive Javadoc documentation guides for Java development, fully compliant with `doclint` (`-Xdoclint:all`) requirements.

## 📚 Documentation Structure

### Full Comprehensive Guides

#### 1. **JAVADOC_GUIDE_EN.md** (English, 2338 lines)
- Complete, production-ready Javadoc guide in English
- 14 detailed sections covering all Java elements
- Covers: Classes, Interfaces, Enums, Records, Annotations, Fields, Methods, Constructors, Generics, Packages, Modules
- Includes extensive good/bad examples
- Full doclint compliance explanations
- Best practices and common mistakes checklist

#### 2. **JAVADOC_GUIDE_RU.md** (Russian, 2335 lines)
- Complete, production-ready Javadoc guide in Russian
- Identical structure and content to English version
- Full translation maintaining technical accuracy
- All examples and checklists included

### LLM System Prompt References

#### 3. **JAVADOC_REFERENCE_FOR_LLM.md** (English, 860 lines)
- **Compact reference guide optimized for LLM context**
- Designed to be used as a system prompt for code generation
- Quick-lookup format with critical rules and examples
- All doclint requirements condensed
- Perfect for AI-assisted Javadoc generation and correction

#### 4. **JAVADOC_REFERENCE_FOR_LLM_RU.md** (Russian, 860 lines)
- **Compact reference guide in Russian for LLM context**
- Same structure as English LLM reference
- Optimized for Russian-speaking LLM applications
- All critical information in condensed format

---

## 🎯 When to Use Each Guide

### For Human Developers
Use **JAVADOC_GUIDE_EN.md** or **JAVADOC_GUIDE_RU.md**:
- Learning Javadoc best practices
- Reference during code reviews
- Team onboarding and training
- Detailed examples and explanations needed
- Understanding the "why" behind rules

### For LLM Integration
Use **JAVADOC_REFERENCE_FOR_LLM.md** or **JAVADOC_REFERENCE_FOR_LLM_RU.md**:
- System prompt for AI code generators
- Context for automated Javadoc generation
- Quick reference for code completion tools
- Token-efficient format for AI applications
- Automated code review systems

---

## ✅ Key Features

### Coverage
- ✅ All Java element types (Classes, Interfaces, Enums, Records, Annotations, Fields, Methods, Constructors)
- ✅ Generic types and type parameters
- ✅ Package documentation (package-info.java)
- ✅ Module documentation (module-info.java)
- ✅ All block tags (@param, @return, @throws, @see, @since, @deprecated)
- ✅ All inline tags ({@code}, {@link}, {@literal}, {@value}, {@inheritDoc}, {@snippet})

### Modern Approach
- ❌ **@author and @version tags discouraged** (use Git instead)
- ✅ Emphasis on @since for version tracking
- ✅ Strict null-handling documentation
- ✅ Thread safety documentation requirements
- ✅ Comprehensive exception documentation

### doclint Compliance
- ✅ Full compliance with `javadoc -Xdoclint:all`
- ✅ HTML tag validation rules
- ✅ Reference validation
- ✅ Complete parameter coverage
- ✅ Return value documentation
- ✅ Exception documentation

---

## 🚀 Quick Start

### For Developers

#### Step 1: Read the Guide
```bash
# English
cat JAVADOC_GUIDE_EN.md

# Russian
cat JAVADOC_GUIDE_RU.md
```

#### Step 2: Validate Your Code
```bash
# Generate Javadoc with full validation
javadoc -Xdoclint:all -d target/javadoc -sourcepath src/main/java -subpackages com.example

# With Maven
mvn javadoc:javadoc -Djavadoc.lint=all

# With Gradle
./gradlew javadoc -Djavadoc.lint=all
```

### For LLM Applications

#### Integration Example
```python
# Load the LLM reference guide
with open('JAVADOC_REFERENCE_FOR_LLM.md', 'r') as f:
    javadoc_reference = f.read()

# Use as system prompt
system_prompt = f"""
You are a Java code documentation expert.
Use the following reference to generate doclint-compliant Javadoc:

{javadoc_reference}

Generate Javadoc for the following code:
"""
```

---

## 📋 Tag Order Reference

### Classes/Interfaces/Enums/Records/Annotations
```
1. @param (type parameters, record components)
2. @see
3. @since
4. @deprecated
```

### Methods/Constructors
```
1. @param (all parameters)
2. @return (non-void methods only)
3. @throws (all exceptions)
4. @see
5. @since
6. @deprecated
```

---

## 🔍 Common doclint Errors

1. **Missing @param** - All method parameters must be documented
2. **Missing @return** - All non-void methods must have @return
3. **Unclosed HTML tags** - All HTML tags must be properly closed
4. **No summary period** - Summary sentence must end with `.`, `!`, or `?`
5. **Invalid references** - All @link and @see references must be valid
6. **Dangling Javadoc** - No blank lines between Javadoc and element

---

## 🎓 Examples

### Minimal Valid Class Documentation
```java
/**
 * Manages user authentication operations.
 * <p>
 * This class is thread-safe.
 *
 * @since 1.0
 */
public class AuthService {
    
    /**
     * Authenticates a user with credentials.
     *
     * @param username the username, must not be null
     * @param password the password, must not be null
     * @return authentication token, never null
     * @throws NullPointerException if username or password is null
     * @throws AuthenticationException if credentials are invalid
     */
    public String authenticate(String username, String password) {
        // implementation
    }
}
```

### Record Documentation
```java
/**
 * Represents an immutable user profile.
 *
 * @param id the unique identifier, must not be null
 * @param name the user name, must not be null or empty
 * @since 2.0
 */
public record UserProfile(String id, String name) {
    /**
     * Compact constructor with validation.
     *
     * @throws NullPointerException if id or name is null
     * @throws IllegalArgumentException if name is empty
     */
    public UserProfile {
        if (id == null || name == null) {
            throw new NullPointerException();
        }
        if (name.isEmpty()) {
            throw new IllegalArgumentException("Name cannot be empty");
        }
    }
}
```

---

## 🤝 Contributing

These guides are production-ready and follow Oracle's official Javadoc standards. If you find any issues or have suggestions for improvements, please open an issue.

---

## 📖 Additional Resources

- [Oracle Javadoc Guide](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html)
- [How to Write Doc Comments](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html)
- [Java SE API Documentation](https://docs.oracle.com/en/java/javase/)

---

## 📄 License

These documentation guides are provided for educational and development purposes.

---

## 📞 Support

For questions about Javadoc best practices or these guides, refer to:
- The full comprehensive guides for detailed explanations
- The LLM reference guides for quick lookup
- Oracle's official Javadoc documentation

---

**Last Updated:** 2024  
**Version:** 1.0  
**Status:** Production Ready ✅
