FROM oven/bun as builder
WORKDIR /usr/src/app
COPY package.json bun.lockb tsconfig.json ./
RUN bun install
RUN bun build

FROM oven/bun as tester
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app /usr/src/app
COPY ./backend ./backend

FROM oven/bun as dev
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app /usr/src/app
COPY ./backend ./backend

FROM node as prod
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app/build/backend /usr/src/app/
ENTRYPOINT [ "node", "index.js" ]