## API Report File for "@backstage/plugin-scaffolder-backend"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts
/// <reference types="node" />

import { BackendFeature } from '@backstage/backend-plugin-api';
import { CatalogApi } from '@backstage/catalog-client';
import { CatalogProcessor } from '@backstage/plugin-catalog-backend';
import { CatalogProcessorEmit } from '@backstage/plugin-catalog-backend';
import { Config } from '@backstage/config';
import { createPullRequest } from 'octokit-plugin-create-pull-request';
import { Entity } from '@backstage/catalog-model';
import express from 'express';
import { GithubCredentialsProvider } from '@backstage/integration';
import { JsonObject } from '@backstage/types';
import { JsonValue } from '@backstage/types';
import { Knex } from 'knex';
import { LocationSpec } from '@backstage/plugin-catalog-backend';
import { Logger } from 'winston';
import { Observable } from '@backstage/types';
import { Octokit } from 'octokit';
import { PluginDatabaseManager } from '@backstage/backend-common';
import { Schema } from 'jsonschema';
import { ScmIntegrationRegistry } from '@backstage/integration';
import { ScmIntegrations } from '@backstage/integration';
import { SpawnOptionsWithoutStdio } from 'child_process';
import { TaskSpec } from '@backstage/plugin-scaffolder-common';
import { TaskSpecV1beta3 } from '@backstage/plugin-scaffolder-common';
import { TemplateInfo } from '@backstage/plugin-scaffolder-common';
import { UrlReader } from '@backstage/backend-common';
import { Writable } from 'stream';

// @public
export type ActionContext<Input extends JsonObject> = {
  logger: Logger;
  logStream: Writable;
  secrets?: TaskSecrets;
  workspacePath: string;
  input: Input;
  output(name: string, value: JsonValue): void;
  createTemporaryDirectory(): Promise<string>;
  templateInfo?: TemplateInfo;
  isDryRun?: boolean;
};

// @public
export const createBuiltinActions: (
  options: CreateBuiltInActionsOptions,
) => TemplateAction<JsonObject>[];

// @public
export interface CreateBuiltInActionsOptions {
  additionalTemplateFilters?: Record<string, TemplateFilter>;
  catalogClient: CatalogApi;
  config: Config;
  integrations: ScmIntegrations;
  reader: UrlReader;
}

// @public
export function createCatalogRegisterAction(options: {
  catalogClient: CatalogApi;
  integrations: ScmIntegrations;
}): TemplateAction<
  | {
      catalogInfoUrl: string;
      optional?: boolean | undefined;
    }
  | {
      repoContentsUrl: string;
      catalogInfoPath?: string | undefined;
      optional?: boolean | undefined;
    }
>;

// @public
export function createCatalogWriteAction(): TemplateAction<{
  filePath?: string | undefined;
  entity: Entity;
}>;

// @public
export function createDebugLogAction(): TemplateAction<{
  message?: string | undefined;
  listWorkspace?: boolean | undefined;
}>;

// @public
export function createFetchPlainAction(options: {
  reader: UrlReader;
  integrations: ScmIntegrations;
}): TemplateAction<{
  url: string;
  targetPath?: string | undefined;
}>;

// @public
export function createFetchTemplateAction(options: {
  reader: UrlReader;
  integrations: ScmIntegrations;
  additionalTemplateFilters?: Record<string, TemplateFilter>;
}): TemplateAction<{
  url: string;
  targetPath?: string | undefined;
  values: any;
  templateFileExtension?: string | boolean | undefined;
  copyWithoutRender?: string[] | undefined;
  copyWithoutTemplating?: string[] | undefined;
  cookiecutterCompat?: boolean | undefined;
}>;

// @public
export const createFilesystemDeleteAction: () => TemplateAction<{
  files: string[];
}>;

// @public
export const createFilesystemRenameAction: () => TemplateAction<{
  files: Array<{
    from: string;
    to: string;
    overwrite?: boolean;
  }>;
}>;

// @public
export function createGithubActionsDispatchAction(options: {
  integrations: ScmIntegrations;
  githubCredentialsProvider?: GithubCredentialsProvider;
}): TemplateAction<{
  repoUrl: string;
  workflowId: string;
  branchOrTagName: string;
  workflowInputs?:
    | {
        [key: string]: string;
      }
    | undefined;
  token?: string | undefined;
}>;

// @public
export function createGithubIssuesLabelAction(options: {
  integrations: ScmIntegrationRegistry;
  githubCredentialsProvider?: GithubCredentialsProvider;
}): TemplateAction<{
  repoUrl: string;
  number: number;
  labels: string[];
  token?: string | undefined;
}>;

// @public
export interface CreateGithubPullRequestActionOptions {
  clientFactory?: (
    input: CreateGithubPullRequestClientFactoryInput,
  ) => Promise<OctokitWithPullRequestPluginClient>;
  githubCredentialsProvider?: GithubCredentialsProvider;
  integrations: ScmIntegrationRegistry;
}

// @public
export type CreateGithubPullRequestClientFactoryInput = {
  integrations: ScmIntegrationRegistry;
  githubCredentialsProvider?: GithubCredentialsProvider;
  host: string;
  owner: string;
  repo: string;
  token?: string;
};

// @public
export function createGithubRepoCreateAction(options: {
  integrations: ScmIntegrationRegistry;
  githubCredentialsProvider?: GithubCredentialsProvider;
}): TemplateAction<{
  repoUrl: string;
  description?: string | undefined;
  homepage?: string | undefined;
  access?: string | undefined;
  deleteBranchOnMerge?: boolean | undefined;
  gitAuthorName?: string | undefined;
  gitAuthorEmail?: string | undefined;
  allowRebaseMerge?: boolean | undefined;
  allowSquashMerge?: boolean | undefined;
  allowMergeCommit?: boolean | undefined;
  requireCodeOwnerReviews?: boolean | undefined;
  requiredStatusCheckContexts?: string[] | undefined;
  repoVisibility?: 'internal' | 'private' | 'public' | undefined;
  collaborators?:
    | (
        | {
            user: string;
            access: 'pull' | 'push' | 'admin' | 'maintain' | 'triage';
          }
        | {
            team: string;
            access: 'pull' | 'push' | 'admin' | 'maintain' | 'triage';
          }
        | {
            username: string;
            access: 'pull' | 'push' | 'admin' | 'maintain' | 'triage';
          }
      )[]
    | undefined;
  token?: string | undefined;
  topics?: string[] | undefined;
}>;

// @public
export function createGithubRepoPushAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
  githubCredentialsProvider?: GithubCredentialsProvider;
}): TemplateAction<{
  repoUrl: string;
  description?: string | undefined;
  defaultBranch?: string | undefined;
  protectDefaultBranch?: boolean | undefined;
  protectEnforceAdmins?: boolean | undefined;
  gitCommitMessage?: string | undefined;
  gitAuthorName?: string | undefined;
  gitAuthorEmail?: string | undefined;
  requireCodeOwnerReviews?: boolean | undefined;
  requiredStatusCheckContexts?: string[] | undefined;
  sourcePath?: string | undefined;
  token?: string | undefined;
}>;

// @public
export function createGithubWebhookAction(options: {
  integrations: ScmIntegrationRegistry;
  defaultWebhookSecret?: string;
  githubCredentialsProvider?: GithubCredentialsProvider;
}): TemplateAction<{
  repoUrl: string;
  webhookUrl: string;
  webhookSecret?: string | undefined;
  events?: string[] | undefined;
  active?: boolean | undefined;
  contentType?: 'form' | 'json' | undefined;
  insecureSsl?: boolean | undefined;
  token?: string | undefined;
}>;

// @public
export function createPublishAzureAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
}): TemplateAction<{
  repoUrl: string;
  description?: string | undefined;
  defaultBranch?: string | undefined;
  sourcePath?: string | undefined;
  token?: string | undefined;
  gitCommitMessage?: string | undefined;
  gitAuthorName?: string | undefined;
  gitAuthorEmail?: string | undefined;
}>;

// @public @deprecated
export function createPublishBitbucketAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
}): TemplateAction<{
  repoUrl: string;
  description?: string | undefined;
  defaultBranch?: string | undefined;
  repoVisibility?: 'private' | 'public' | undefined;
  sourcePath?: string | undefined;
  enableLFS?: boolean | undefined;
  token?: string | undefined;
  gitCommitMessage?: string | undefined;
  gitAuthorName?: string | undefined;
  gitAuthorEmail?: string | undefined;
}>;

// @public
export function createPublishBitbucketCloudAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
}): TemplateAction<{
  repoUrl: string;
  description?: string | undefined;
  defaultBranch?: string | undefined;
  repoVisibility?: 'private' | 'public' | undefined;
  sourcePath?: string | undefined;
  token?: string | undefined;
}>;

// @public
export function createPublishBitbucketServerAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
}): TemplateAction<{
  repoUrl: string;
  description?: string | undefined;
  defaultBranch?: string | undefined;
  repoVisibility?: 'private' | 'public' | undefined;
  sourcePath?: string | undefined;
  enableLFS?: boolean | undefined;
  token?: string | undefined;
}>;

// @public
export function createPublishGerritAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
}): TemplateAction<{
  repoUrl: string;
  description: string;
  defaultBranch?: string | undefined;
  gitCommitMessage?: string | undefined;
  gitAuthorName?: string | undefined;
  gitAuthorEmail?: string | undefined;
  sourcePath?: string | undefined;
}>;

// @public
export function createPublishGerritReviewAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
}): TemplateAction<{
  repoUrl: string;
  branch?: string | undefined;
  sourcePath?: string | undefined;
  gitCommitMessage?: string | undefined;
  gitAuthorName?: string | undefined;
  gitAuthorEmail?: string | undefined;
}>;

// @public
export function createPublishGithubAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
  githubCredentialsProvider?: GithubCredentialsProvider;
}): TemplateAction<{
  repoUrl: string;
  description?: string | undefined;
  homepage?: string | undefined;
  access?: string | undefined;
  defaultBranch?: string | undefined;
  protectDefaultBranch?: boolean | undefined;
  protectEnforceAdmins?: boolean | undefined;
  deleteBranchOnMerge?: boolean | undefined;
  gitCommitMessage?: string | undefined;
  gitAuthorName?: string | undefined;
  gitAuthorEmail?: string | undefined;
  allowRebaseMerge?: boolean | undefined;
  allowSquashMerge?: boolean | undefined;
  allowMergeCommit?: boolean | undefined;
  sourcePath?: string | undefined;
  requireCodeOwnerReviews?: boolean | undefined;
  requiredStatusCheckContexts?: string[] | undefined;
  repoVisibility?: 'internal' | 'private' | 'public' | undefined;
  collaborators?:
    | (
        | {
            user: string;
            access: 'pull' | 'push' | 'admin' | 'maintain' | 'triage';
          }
        | {
            team: string;
            access: 'pull' | 'push' | 'admin' | 'maintain' | 'triage';
          }
        | {
            username: string;
            access: 'pull' | 'push' | 'admin' | 'maintain' | 'triage';
          }
      )[]
    | undefined;
  token?: string | undefined;
  topics?: string[] | undefined;
}>;

// @public
export const createPublishGithubPullRequestAction: ({
  integrations,
  githubCredentialsProvider,
  clientFactory,
}: CreateGithubPullRequestActionOptions) => TemplateAction<{
  title: string;
  branchName: string;
  description: string;
  repoUrl: string;
  draft?: boolean | undefined;
  targetPath?: string | undefined;
  sourcePath?: string | undefined;
  token?: string | undefined;
  reviewers?: string[] | undefined;
  teamReviewers?: string[] | undefined;
}>;

// @public
export function createPublishGitlabAction(options: {
  integrations: ScmIntegrationRegistry;
  config: Config;
}): TemplateAction<{
  repoUrl: string;
  defaultBranch?: string | undefined;
  repoVisibility?: 'internal' | 'private' | 'public' | undefined;
  sourcePath?: string | undefined;
  token?: string | undefined;
  gitCommitMessage?: string | undefined;
  gitAuthorName?: string | undefined;
  gitAuthorEmail?: string | undefined;
  setUserAsOwner?: boolean | undefined;
}>;

// @public
export const createPublishGitlabMergeRequestAction: (options: {
  integrations: ScmIntegrationRegistry;
}) => TemplateAction<{
  repoUrl: string;
  title: string;
  description: string;
  branchName: string;
  targetPath: string;
  token?: string | undefined;
  commitAction?: 'update' | 'create' | 'delete' | undefined;
  projectid?: string | undefined;
  removeSourceBranch?: boolean | undefined;
  assignee?: string | undefined;
}>;

// @public
export function createRouter(options: RouterOptions): Promise<express.Router>;

// @public
export const createTemplateAction: <TInput extends JsonObject>(
  templateAction: TemplateAction<TInput>,
) => TemplateAction<TInput>;

// @public
export type CreateWorkerOptions = {
  taskBroker: TaskBroker;
  actionRegistry: TemplateActionRegistry;
  integrations: ScmIntegrations;
  workingDirectory: string;
  logger: Logger;
  additionalTemplateFilters?: Record<string, TemplateFilter>;
};

// @public
export interface CurrentClaimedTask {
  createdBy?: string;
  secrets?: TaskSecrets;
  spec: TaskSpec;
  taskId: string;
}

// @public
export class DatabaseTaskStore implements TaskStore {
  // (undocumented)
  claimTask(): Promise<SerializedTask | undefined>;
  // (undocumented)
  completeTask({
    taskId,
    status,
    eventBody,
  }: {
    taskId: string;
    status: TaskStatus;
    eventBody: JsonObject;
  }): Promise<void>;
  // (undocumented)
  static create(options: DatabaseTaskStoreOptions): Promise<DatabaseTaskStore>;
  // (undocumented)
  createTask(
    options: TaskStoreCreateTaskOptions,
  ): Promise<TaskStoreCreateTaskResult>;
  // (undocumented)
  emitLogEvent(
    options: TaskStoreEmitOptions<
      {
        message: string;
      } & JsonObject
    >,
  ): Promise<void>;
  // (undocumented)
  getTask(taskId: string): Promise<SerializedTask>;
  // (undocumented)
  heartbeatTask(taskId: string): Promise<void>;
  // (undocumented)
  list(options: { createdBy?: string }): Promise<{
    tasks: SerializedTask[];
  }>;
  // (undocumented)
  listEvents({ taskId, after }: TaskStoreListEventsOptions): Promise<{
    events: SerializedTaskEvent[];
  }>;
  // (undocumented)
  listStaleTasks({ timeoutS }: { timeoutS: number }): Promise<{
    tasks: {
      taskId: string;
    }[];
  }>;
}

// @public
export type DatabaseTaskStoreOptions = {
  database: PluginDatabaseManager | Knex;
};

// @public
export const executeShellCommand: (options: RunCommandOptions) => Promise<void>;

// @public
export function fetchContents({
  reader,
  integrations,
  baseUrl,
  fetchUrl,
  outputPath,
}: {
  reader: UrlReader;
  integrations: ScmIntegrations;
  baseUrl?: string;
  fetchUrl?: string;
  outputPath: string;
}): Promise<void>;

// @public (undocumented)
export type OctokitWithPullRequestPluginClient = Octokit & {
  createPullRequest(options: createPullRequest.Options): Promise<{
    data: {
      html_url: string;
      number: number;
    };
  } | null>;
};

// @public
export interface RouterOptions {
  // (undocumented)
  actions?: TemplateAction<any>[];
  // (undocumented)
  additionalTemplateFilters?: Record<string, TemplateFilter>;
  // (undocumented)
  catalogClient: CatalogApi;
  // (undocumented)
  config: Config;
  // (undocumented)
  database: PluginDatabaseManager;
  // (undocumented)
  logger: Logger;
  // (undocumented)
  reader: UrlReader;
  // (undocumented)
  taskBroker?: TaskBroker;
  // (undocumented)
  taskWorkers?: number;
}

// @public (undocumented)
export type RunCommandOptions = {
  command: string;
  args: string[];
  options?: SpawnOptionsWithoutStdio;
  logStream?: Writable;
};

// @alpha
export const scaffolderCatalogModule: (options?: unknown) => BackendFeature;

// @public (undocumented)
export class ScaffolderEntitiesProcessor implements CatalogProcessor {
  // (undocumented)
  getProcessorName(): string;
  // (undocumented)
  postProcessEntity(
    entity: Entity,
    _location: LocationSpec,
    emit: CatalogProcessorEmit,
  ): Promise<Entity>;
  // (undocumented)
  validateEntityKind(entity: Entity): Promise<boolean>;
}

// @public
export type SerializedTask = {
  id: string;
  spec: TaskSpec;
  status: TaskStatus;
  createdAt: string;
  lastHeartbeatAt?: string;
  createdBy?: string;
  secrets?: TaskSecrets;
};

// @public
export type SerializedTaskEvent = {
  id: number;
  taskId: string;
  body: JsonObject;
  type: TaskEventType;
  createdAt: string;
};

// @public
export interface TaskBroker {
  // (undocumented)
  claim(): Promise<TaskContext>;
  // (undocumented)
  dispatch(
    options: TaskBrokerDispatchOptions,
  ): Promise<TaskBrokerDispatchResult>;
  // (undocumented)
  event$(options: { taskId: string; after: number | undefined }): Observable<{
    events: SerializedTaskEvent[];
  }>;
  // (undocumented)
  get(taskId: string): Promise<SerializedTask>;
  // (undocumented)
  list?(options?: { createdBy?: string }): Promise<{
    tasks: SerializedTask[];
  }>;
  // (undocumented)
  vacuumTasks(options: { timeoutS: number }): Promise<void>;
}

// @public
export type TaskBrokerDispatchOptions = {
  spec: TaskSpec;
  secrets?: TaskSecrets;
  createdBy?: string;
};

// @public
export type TaskBrokerDispatchResult = {
  taskId: string;
};

// @public
export type TaskCompletionState = 'failed' | 'completed';

// @public
export interface TaskContext {
  // (undocumented)
  complete(result: TaskCompletionState, metadata?: JsonObject): Promise<void>;
  // (undocumented)
  createdBy?: string;
  // (undocumented)
  done: boolean;
  // (undocumented)
  emitLog(message: string, logMetadata?: JsonObject): Promise<void>;
  // (undocumented)
  getWorkspaceName(): Promise<string>;
  // (undocumented)
  isDryRun?: boolean;
  // (undocumented)
  secrets?: TaskSecrets;
  // (undocumented)
  spec: TaskSpec;
}

// @public
export type TaskEventType = 'completion' | 'log';

// @public
export class TaskManager implements TaskContext {
  // (undocumented)
  complete(result: TaskCompletionState, metadata?: JsonObject): Promise<void>;
  // (undocumented)
  static create(
    task: CurrentClaimedTask,
    storage: TaskStore,
    logger: Logger,
  ): TaskManager;
  // (undocumented)
  get createdBy(): string | undefined;
  // (undocumented)
  get done(): boolean;
  // (undocumented)
  emitLog(message: string, logMetadata?: JsonObject): Promise<void>;
  // (undocumented)
  getWorkspaceName(): Promise<string>;
  // (undocumented)
  get secrets(): TaskSecrets | undefined;
  // (undocumented)
  get spec(): TaskSpecV1beta3;
}

// @public
export type TaskSecrets = Record<string, string> & {
  backstageToken?: string;
};

// @public
export type TaskStatus =
  | 'open'
  | 'processing'
  | 'failed'
  | 'cancelled'
  | 'completed';

// @public
export interface TaskStore {
  // (undocumented)
  claimTask(): Promise<SerializedTask | undefined>;
  // (undocumented)
  completeTask(options: {
    taskId: string;
    status: TaskStatus;
    eventBody: JsonObject;
  }): Promise<void>;
  // (undocumented)
  createTask(
    options: TaskStoreCreateTaskOptions,
  ): Promise<TaskStoreCreateTaskResult>;
  // (undocumented)
  emitLogEvent({ taskId, body }: TaskStoreEmitOptions): Promise<void>;
  // (undocumented)
  getTask(taskId: string): Promise<SerializedTask>;
  // (undocumented)
  heartbeatTask(taskId: string): Promise<void>;
  // (undocumented)
  list?(options: { createdBy?: string }): Promise<{
    tasks: SerializedTask[];
  }>;
  // (undocumented)
  listEvents({ taskId, after }: TaskStoreListEventsOptions): Promise<{
    events: SerializedTaskEvent[];
  }>;
  // (undocumented)
  listStaleTasks(options: { timeoutS: number }): Promise<{
    tasks: {
      taskId: string;
    }[];
  }>;
}

// @public
export type TaskStoreCreateTaskOptions = {
  spec: TaskSpec;
  createdBy?: string;
  secrets?: TaskSecrets;
};

// @public
export type TaskStoreCreateTaskResult = {
  taskId: string;
};

// @public
export type TaskStoreEmitOptions<TBody = JsonObject> = {
  taskId: string;
  body: TBody;
};

// @public
export type TaskStoreListEventsOptions = {
  taskId: string;
  after?: number | undefined;
};

// @public
export class TaskWorker {
  // (undocumented)
  static create(options: CreateWorkerOptions): Promise<TaskWorker>;
  // (undocumented)
  runOneTask(task: TaskContext): Promise<void>;
  // (undocumented)
  start(): void;
}

// @public (undocumented)
export type TemplateAction<Input extends JsonObject> = {
  id: string;
  description?: string;
  supportsDryRun?: boolean;
  schema?: {
    input?: Schema;
    output?: Schema;
  };
  handler: (ctx: ActionContext<Input>) => Promise<void>;
};

// @public
export class TemplateActionRegistry {
  // (undocumented)
  get(actionId: string): TemplateAction<JsonObject>;
  // (undocumented)
  list(): TemplateAction<JsonObject>[];
  // (undocumented)
  register<TInput extends JsonObject>(action: TemplateAction<TInput>): void;
}

// @public (undocumented)
export type TemplateFilter = (...args: JsonValue[]) => JsonValue | undefined;
```
