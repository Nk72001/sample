FROM elixir:latest

# Install Hex and Rebar
RUN mix local.hex --force && \
    mix local.rebar --force

# Set environment variables
ENV MIX_ENV=prod \
    LANG=C.UTF-8

# Create and set the working directory
WORKDIR /app

# Copy the mix files
COPY mix.exs mix.lock ./

# Install dependencies
RUN mix deps.get --only prod

# Copy the rest of the application code
COPY . .

# Compile the application
RUN mix deps.compile && \
    mix compile

# Create a dummy assets/package.json
RUN mkdir -p assets && \
    echo "{}" > assets/package.json

# Build the Phoenix application
RUN mix phx.digest

# Expose the port on which the Phoenix app will run
EXPOSE 4000

# Set the entry point to start the Phoenix server
CMD ["mix", "phx.server"]