.PHONY: all clean tests lint build format coverage benchmarks

all: build tests lint

# Run tests with coverage
tests:
	@echo "Running tests with coverage..."
	go test -v -race -covermode=atomic -coverprofile=coverage.out ./...
	@go tool cover -func=coverage.out
	@if command -v go tool cover > /dev/null 2>&1; then \
		go tool cover -html=coverage.out -o coverage.html; \
	fi

# Run benchmarks
benchmarks:
	@echo "Running benchmarks..."
	go test -run=^$$ -bench=. -benchmem ./...

# Build the package
build:
	@echo "Building package..."
	go build ./...

# Format code
format:
	@echo "Formatting code..."
	gofmt -s -w .

# Lint code
lint:
	@echo "Linting code..."
	@if command -v golangci-lint >/dev/null 2>&1; then \
		golangci-lint run ./...; \
	else \
		echo "golangci-lint not installed, skipping lint"; \
	fi

# Clean build artifacts
clean:
	@echo "Cleaning build artifacts..."
	@find . -type f -name "*.test" -delete
	@find . -type f -name "coverage.out" -delete
	@find . -type f -name "coverage.html" -delete
	@find . -type d -name "vendor" -exec rm -rf {} + 2>/dev/null || true
